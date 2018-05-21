========================================================================
Provisioning hot swap use case using Dell EMC Networking Ansible modules
========================================================================

This example use case topology includes a simple two-tier CLOS fabric with 2 spines and 4 leafs. These steps will show how you Spine 2 will be hot swapped without traffic loss.

.. figure:: ./_static/topo.png
   :scale: 50 %
   :alt: map to buried treasure

Create simple Ansible playbook
------------------------------

- Part 1 - covers creating an inventory file and host variable file for spine2, creating a pre-step hot swap playbook, then running the playbook
- Part 2 - covers creating an inventory file and host variable file for each leaf (4), creating a playbook to delete the ecmp path for spine2 from each leaf, then running the playbook
- Part 3 - covers replacing spine2 with a new switch, booting an OS10 image, creating inventory and host variable files for the new spine2, creating a post hot swap playbook, then running the playbook

Part 1
~~~~~~

Refer to the CLOS fabric example to configure a 6 node CLOS fabric with EBGP. Use the example and run the playbook. 

Create an inventory file called *inventory.yaml*, then specify the device IP address for spine2.

::

    spine2 ansible_host=10.16.204.57 

    [spine]
    spine2

    [leaf]

    [datacenter:children]
    spine

Create a host variable file called ``host_vars/spine2.yaml``, then define the host and credentials.

    - Take a backup of the running configuration to a remote location
    - Shut down the BGP neighbors in the hot swap switch to avoid traffic drop

:: 

    hostname: spine2
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10

    copy_running_remote:
        - copy_type: scp
          username: linuxadmin
          password: linuxadmin
          host_ip: 10.16.204.62
          file_path: /home/linuxadmin/running-config

    dellos_bgp:
        asn: 64901
        neighbor:
          - type: ipv4
            remote_asn: 64801
            ip: 100.2.1.2
            admin: down
            state: present
          - type: ipv4
            remote_asn: 64802
            ip: 100.2.33.2
            admin: down
            state: present
          - type: ipv4
            remote_asn: 64803
            ip: 100.2.17.2
            admin: down
            state: present
          - type: ipv4
            remote_asn: 64804
            ip: 100.2.49.2
            admin: down
            state: present
          - type: ipv6
            remote_asn: 64801
            ip: 2001:100:2:1::2
            admin: down
            state: present
          - type: ipv6
            remote_asn: 64802
            ip: 2001:100:2:11::2
            admin: down
            state: present
          - type: ipv6
            remote_asn: 64803
            ip: 2001:100:2:21::2
            admin: down
            state: present
          - type: ipv6
            remote_asn: 64804
            ip: 2001:100:2:31::2
            admin: down
            state: present
        state: present

Create a playbook called ``hot_swap_pre_step.yaml``:

::

  ---
  - hosts: datacenter
    gather_facts: no
    connection: network_cli
      tasks:
        - name: Assembling configfurations
          assemble: src={{ build_dir }} dest={{ build_dir }}/{{hostname}}.conf regexp='\\S_{{hostname}}\\S'
        - name: "copy running config to remote location"
          dellos10_command:
            commands:
               - command: 'copy running-configuration {{item.copy_type}}://{{item.username}}:{{item.password}}@{{item.host_ip}}:{{item.file_path}}'
                 #If the switch asks for credentials for copy command, use the below commented statements to give the prompt and password
                 #prompt: 'admin:'
                 #answer: 'admin'
          with_items: '{{copy_running_remote}}'
  - hosts: datacenter
    connection: network_cli
    vars:
      build_dir: "/root/debug"
    roles:
      - Dell-Networking.dellos-bgp

Run the playbook.

``ansible-playbook -i inventory.yaml hot_swap_pre_step.yaml``

Part 2
~~~~~~

1. After shutting the neighborship in the spine2 switch, check if the ECMP path to spine2 is deleted in each of the leaf switches.

Create an inventory file called ``inventory.yaml``, then specify the device IP address of all leaf switches:

::

    leaf1 ansible_host=10.16.204.27 
    leaf2 ansible_host=10.16.204.28 
    leaf3 ansible_host=10.16.204.29 
    leaf4 ansible_host=10.16.204.30

    [spine]

    [leaf]
    leaf1
    leaf2
    leaf3
    leaf4

    [datacenter:children]
    leaf

Create a host variable file called ``host_vars/leaf1.yaml``, then define the host and credentials. The remote_neighbor_ip is the EBGP neighbor IP of spine2 with each of each leaf switch (see the CLOS fabric example for EBGP configuration):

:: 

    hostname: leaf1
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10

    remote_neighbor_ip: "100.2.1.1"


Create a host variable file called ``host_vars/leaf2.yaml``, then define the host and credentials:

::

    hostname: leaf2
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10

    remote_neighbor_ip: "100.2.17.1"


Create a host variable file called ``host_vars/leaf3.yaml``, then define the host and credentials:

:: 

    hostname: leaf3
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10

    remote_neighbor_ip: "100.2.33.1"


Create a host variable file called ``host_vars/leaf4.yaml``, then define the host and credentials:

::


    hostname: leaf4
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10

    remote_neighbor_ip: "100.2.49.1"


Create a playbook called ``waitfor_ecmp_path_delete.yaml``

.. note:: A debug message will print when the ECMP path for spine2 is deleted in each of the leaf switches.

:: 

  ---
  - hosts: datacenter
    gather_facts: no
    connection: network_cli
    vars:
      build_dir: "/root/debug"
    tasks:
      - name: Assembling configfurations
          assemble: src={{ build_dir }} dest={{ build_dir }}/{{hostname}}.conf regexp='\\S_{{hostname}}\\S'
      - name: "Wait for spine2 routes delete in {{ hostname }}"
          dellos10_command:
            commands:
               - command: "show ip route bgp | grep {{ remote_neighbor_ip }}"
        retries: 10
        delay: 5
        register: result
        until: result.stdout[0] == ""
      - debug:
          msg: "{{ hostname }} has deleted the ECMP to spine2 switch"
        when: result.stdout[0] == ""  

#. Execute the playbook.

``ansible-playbook -i inventory.yaml waitfor_ecmp_path_delete.yaml``

Part 3
~~~~~~

1. After checking the spine2 ECMP path deletion in all leaf switches, replace spine2 with a new switch. The new spine2 switch should be connected as the old spine switch after it boots up with an OS10 image.

    - Manually assign the same spine2 management IP address (for example, 10.16.204.57)
    - Use the Management IP provided by the DHCP server

#. Create an inventory file called *inventory.yaml*, then specify the device IP address for spine2. The device IP can be same spine2 IP or an IP obtained from the DHCP server (x.x.x.x).

:: 

    spine2 ansible_host=x.x.x.x 

    [spine]
    spine2

    [leaf]

    [datacenter:children]
    spine


#. Create a host variable file called *host_vars/spine2.yaml*, then define the host, credentials, and apply the same backup configuration that was saved earlier.

:: 

    hostname: spine2
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10

    copy_remote_running:
        - copy_type: scp
          username: linuxadmin
          password: linuxadmin
          host_ip: 10.16.204.62
          file_path: /home/linuxadmin/running-config


Create a playbook called ``hot_swap_post_step.yaml``

:: 

  ---
  - hosts: datacenter
    gather_facts: no
    connection: network_cli
      tasks:
        - name: Assembling configfurations
          assemble: src={{ build_dir }} dest={{ build_dir }}/{{hostname}}.conf regexp='\\S_{{hostname}}\\S'
        - name: "copy running config to remote location"
          dellos10_command:
            commands:
               - command: 'copy {{item.copy_type}}://{{item.username}}:{{item.password}}@{{item.host_ip}}:{{item.file_path}} running-configuration'
                 #If the switch asks for credentials for copy command, use the below commented statements to give the prompt and password
                 #prompt: 'admin:'
                 #answer: 'admin'
          with_items: '{{copy_remote_running}}'


Execute the playbook:

::

  ansible-playbook -i inventory.yaml hot_swap_post_step.yaml
  
(c) 2017 Dell Inc. or its subsidiaries. All Rights Reserved.  

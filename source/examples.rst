########################################### 
Dell EMC Networking Ansible module examples
###########################################

These module examples explain how to create a simple Ansible playbook, run the Dell EMC Networking Ansible modules, then configure a switch using Ansible roles.

Create simple Ansible playbook
******************************

1. Create an inventory file called *inventory.yaml* and specify the IP address.

::

    spine1 ansible_host=10.11.182.16

2. Create a host variable file called *host_vars/spine1.yaml* then define the host, credentials, and transport.

::

    hostname: spine1
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_become_method: enable
    ansible_become: yes
    ansible_become_pass: xxxxx
    ansible_network_os: xxxxx


3. Create a playbook called *showver.yaml*.

::

  hosts: spine1
  connection: network_cli
  gather_facts: no

  tasks:
  - name: "Get Dell EMC OS9 Show version"
    dellos9_command:
      commands: ['show version']
    register: show_ver

  - debug: var=show_ver

4. Run the playbook

::

    ansible-playbook -i inventory.yaml showver.yaml

Run Dell EMC Networking Ansible examples
****************************************

Use these sample Ansible playbooks to understand how to use Dell EMC Networking Ansible modules.

Installation and setup
======================

1. Install `Ansible <http://docs.ansible.com/ansible/intro_installation.html>`_.

2. Clone the `Ansible-dellos-examples <https://github.com/Dell-Networking/ansible-dellos-examples>`_ repository in the control machine.

3. Update the *inventory.yaml* file to configure the device IP.

4. Update the corresponding host variables (use *hosts_var/dellos10_sw1.yaml* for device credentials).

OS6
---

dellos6_facts module that collects the facts from the OS6 device example

::

    ansible-playbook -i inventory.yaml getfacts_os6.yaml

dellos6_command module that executes the show version command example

::

    ansible-playbook -i inventory.yaml showver_os6.yaml

dellos6_config module that configures the hostname on the OS6 device example

:: 

    ansible-playbook -vvv -i inventory.yaml hostname_os6.yaml

OS9
---

dellos9_facts module that collects the facts from the OS9 device example

::

    ansible-playbook -i inventory.yaml getfacts_os9.yaml

dellos9_command module that executes the show version command example

::

    ansible-playbook -i inventory.yaml showver_os9.yaml

dellos9_config module that configures the hostname on the OS9 device example

::

    ansible-playbook -vvv -i inventory.yaml hostname_os9.yaml

OS10
----

dellos10_facts module that collects the facts from the OS10 device example

::

    ansible-playbook -i inventory.yaml getfacts_os10.yaml

dellos10_command module that executes the show version command example

::

    ansible-playbook -i inventory.yaml showver_os10.yaml

dellos10_config module that configures the hostname on the OS10 device example

::

    ansible-playbook -vvv -i inventory.yaml hostname_os10.yaml

Playbook using Ansible roles example
************************************

Use these examples to configure the switch using Ansible roles.

1. Create an inventory file called *inventory.yaml* and specify the device IP address.

::

    spine1 ansible_host= <ip_address> 

2. Create a host variable file called *host_vars/spine1.yaml* then define the host, credentials, and transport.

::

	---
	hostname: dellos9

        ansible_ssh_user: xxxxx
        ansible_ssh_pass: xxxxx
        ansible_become: yes
        ansible_become_method: enable
        ansible_become_pass: xxxxx
        ansible_network_os: dellos9

	
	dellos_interface:
		fortyGigE 0/32:
		  desc: "Connected to Spine1"
		  portmode:
		  switchport: False
		  mtu: 2500
		  admin: up
		  ipv6_and_mask: 2001:4898:5808:ffa2::5/126
		  suppress_ra : present
		  ip_type_dynamic: true
		  ip_and_mask: 192.168.23.22/24
		  class_vendor_identifier: present
		  option82: true
		  remote_id: hostname
		fortyGigE 0/20:
		  portmode:
		  switchport: False
		fortyGigE 0/64:
		  portmode:
		  switchport: True
		fortyGigE 0/60:
		  portmode:
		  switchport: True
		fortyGigE 0/12:
		  portmode:
		  switchport: True
		loopback 0:
		  ip_and_mask: 1.1.1.1/32
		  admin: up
		Port-channel 12:
		  switchport: True
	dellos_vlan:
		vlan 100:
		  name: "Mgmt Network"
		  description: "Int-vlan"
		  tagged_members:
			- port: fortyGigE 0/60
			  state: present
		  untagged_members:
			- port: fortyGigE 0/12
			  state: present
		  state: present

3. Create a playbook called *switch_config.yaml*.

::

	---
	- hosts: dellos9
	  gather_facts: no
	  connection: network_cli
	  roles:		
		- Dell-Networking.dellos-interface
		- Dell-Networking.dellos-vlan

4. Run the playbook.

::

    ansible-playbook -i inventory.yaml switch_config.yaml

===============================================
Examples of Dell EMC Networking Ansible Modules
===============================================

Creating a Simple Ansible Playbook
-----------------------------------

STEP 1
~~~~~~~

Create a inventory file ``inventory.yaml`` and specify the device IP address:
    
:: 

   spine1 ansible_host=10.11.182.16

STEP 2
~~~~~~~

Create a host variable file ``host_vars/spine1.yaml`` and define the host, credentials, and transport:
    
:: 

    hostname: spine1
    provider:
      host: "{{ hostname }}"
      username: xxxxx
      password: xxxxx
      authorize: yes
      auth_pass: xxxxx
      transport: cli

STEP 3
~~~~~~~

Create a playbook ``showver.yaml``:


:: 

  hosts: spine1
  connection: local
  gather_facts: no

  tasks:
  - name: "Get Dell EMC OS9 Show version"
    dellos9_command:
      commands: ['show version']
      provider: "{{ cli }}"
    register: show_ver

  - debug: var=show_ver


STEP 4
~~~~~~

Execute the playbook:

``ansible-playbook -i inventory.yaml showver.yaml``


Running Dell EMC Networking Ansible Examples
---------------------------------------------

Use these sample Ansible playbooks to understand how to use Dell EMC Networking Ansible modules.

Installation and Setup
~~~~~~~~~~~~~~~~~~~~~~

1. Install Ansible. See `Ansible documentation <http://docs.ansible.com/ansible/intro_installation.html>`_.
2. Clone the `Dell EMC Ansible Example <https://github.com/Dell-Networking/ansible-dellos-examples>`_ repository in the Control Machine.
3. Update the ``inventory.yaml`` file to configure the device IP.
4. Update the corresponding host variables (for example: ``hosts_var/dellos10_sw1.yaml`` for device credentials).


Dell EMC Networking OS6
~~~~~~~~~~~~~~~~~~~~~~~~~

Example for dellos6_facts module that collects the facts from the OS6 device:

``ansible-playbook -i inventory.yaml getfacts_os6.yaml``

Example for dellos6_command module that executes the show version command:

``ansible-playbook -i inventory.yaml showver_os6.yaml``

Example for dellos6_config module that configures the hostname on the OS6 device:

``ansible-playbook -vvv -i inventory.yaml hostname_os6.yaml``


Dell EMC Networking OS9
~~~~~~~~~~~~~~~~~~~~~~~~~

Example for dellos9_facts module that collects the facts from the OS9 device:

``ansible-playbook -i inventory.yaml getfacts_os9.yaml``

Example for dellos9_command module that executes the show version command:

``ansible-playbook -i inventory.yaml showver_os9.yaml``

Example for dellos9_config module that configures the hostname on the OS9 device:

``ansible-playbook -vvv -i inventory.yaml hostname_os9.yaml``


Dell EMC Networking OS10
~~~~~~~~~~~~~~~~~~~~~~~~~

Example for dellos10_facts module that collects the facts from the OS10 device:

``ansible-playbook -i inventory.yaml getfacts_os10.yaml``

Example for dellos10_command module that executes the show version command:

``ansible-playbook -i inventory.yaml showver_os10.yaml``

Example for dellos10_config module that configures the hostname on the OS10 device:

``ansible-playbook -vvv -i inventory.yaml hostname_os10.yaml``

Example Playbook using Ansible Roles
------------------------------------

The following examples shows how to use the Ansible Roles to configure the switch

STEP 1
~~~~~~~

Create a inventory file ``inventory.yaml`` and specify the device IP address:
    
:: 

   spine1 ansible_host= <ip_address> ansible_net_os_name= <OS name(dellos9)>

STEP 2
~~~~~~~

Create a host variable file ``host_vars/spine1.yaml`` and define the host, credentials, and transport:
    
:: 

	---
	hostname: dellos9

	cli:
	  host: "{{ ansible_host }}"
	  username: "{{ dellos9_cli_user | default('admin') }}"
	  password: "{{ dellos9_cli_pass | default('admin') }}"
	  authorize: true
	  auth_pass: "{{ dellos9_cli_en_pass | default('ansible') }}"
	  transport: cli

	
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

STEP 3
~~~~~~~

Create a playbook ``switch_config.yaml``:


:: 

	---
	- hosts: dellos9
	  gather_facts: no
	  connection: local
	  roles:		
		- Dell-Networking.dellos-interface
		- Dell-Networking.dellos-vlan


STEP 4
~~~~~~

Execute the playbook:

``ansible-playbook -i inventory.yaml switch_config.yaml``


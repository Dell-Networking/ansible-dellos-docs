 
==============
Installation
==============


Control Machine
----------------


Dell EMC Networking Ansible Modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dell EMC Networking Ansible modules are part of Ansible Core. Install Ansible 2.2 or later to use these modules. For more information, see `Ansible documentation <http://docs.ansible.com/ansible/intro_installation.html>`_.


Dell EMC Networking Ansible Roles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To install all the Dell EMC Networking Ansible roles use the following command:

 ``ansible-galaxy install -r dellemc_roles.txt``

Where ``dellemc_roles.txt`` is defined as:: 

	Dell-Networking.dellos.aaa
	Dell-Networking.dellos.acl
	Dell-Networking.dellos.dcb
	Dell-Networking.dellos.dns
	Dell-Networking.dellos.ecmp
	Dell-Networking.dellos.lldp	
	Dell-Networking.dellos.prefix-list
	Dell-Networking.dellos.sflow
	Dell-Networking.dellos.vlt
	Dell-Networking.dellos.vrf
	Dell-Networking.dellos.vrrp
	Dell-Networking.dellos.snmp
	Dell-Networking.dellos.users
	Dell-Networking.dellos.logging
	Dell-Networking.dellos.bgp
	Dell-Networking.dellos.interface
	Dell-Networking.dellos.lag
	Dell-Networking.dellos.system
	Dell-Networking.dellos.vlan
	Dell-Networking.dellos.xstp

You can also install a specific Dell EMC Networking Ansible role using one of the following commands:

	``ansible-galaxy install Dell-Networking.dellos.aaa``
	
	``ansible-galaxy install Dell-Networking.dellos.acl``
	
	``ansible-galaxy install Dell-Networking.dellos.dcb``
	
	``ansible-galaxy install Dell-Networking.dellos.dns``
	
	``ansible-galaxy install Dell-Networking.dellos.ecmp``
	
	``ansible-galaxy install Dell-Networking.dellos.lldp``
	
	``ansible-galaxy install Dell-Networking.dellos.prefix-list``
	
	``ansible-galaxy install Dell-Networking.dellos.sflow``
	
	``ansible-galaxy install Dell-Networking.dellos.vlt``
	
	``ansible-galaxy install Dell-Networking.dellos.vrf``
	
	``ansible-galaxy install Dell-Networking.dellos.vrrp``
	
	``ansible-galaxy install Dell-Networking.dellos.snmp``
	
	``ansible-galaxy install Dell-Networking.dellos.users``
	
	``ansible-galaxy install Dell-Networking.dellos.logging``
	
	``ansible-galaxy install Dell-Networking.dellos.bgp``
	
	``ansible-galaxy install Dell-Networking.dellos.interface``
	
	``ansible-galaxy install Dell-Networking.dellos.lag``
	
	``ansible-galaxy install Dell-Networking.dellos.system``
	
	``ansible-galaxy install Dell-Networking.dellos.vlan``
	
	``ansible-galaxy install Dell-Networking.dellos.xstp``
	

For more information on the Dell EMC Networking Ansible roles, see `Ansible Galaxy <https://galaxy.ansible.com/Dell-Networking/>`_.


Dell EMC Networking Devices
----------------------------

Dell EMC Networking devices require minimal configuration to run Ansible playbooks.


OS6
~~~

1. Create a username and password for Ansible.
2. Configure the management interface (for example, static/dynamic IP address).
3. Enable the SSH server.

:: 

	console(config)#username admin password ansible@123
	console(config)#enable password ansible@123
	console(config)#interface  out-of-band
	console(config-if)#ip address 10.16.148.79 255.255.255.0 10.16.148.254 
	console(config-if)#exit
	console(config)#ip ssh  server 

OS9
~~~

1. Create a username and password for Ansible.
2. Configure the management interface (for example, static/dynamic IP address).
3. Enable the SSH server.
4. Set the maximum connection rate limit.

:: 

   Dell(conf)#username ansible password ansible
   Dell(conf)#enable password ansible
   Dell(conf)#interface managementethernet 0/0
   Dell(conf-if-ma-0/0)#ip add 10.16.148.72/24
   Dell(conf-if-ma-0/0)#no shutdown 
   Dell(conf-if-ma-0/0)#exit
   Dell(conf)#ip ssh server enable 
   Dell(conf)#ip ssh connection-rate-limit 60

OS10
~~~~

1. Create a username and password for Ansible.
2. Configure the management interface (for example, static/dynamic IP address).

:: 

	OS10(config)# username ansible password ansible
	OS10(config)# interface mgmt 1/1/1
	OS10(conf-if-ma-1/1/1)# ip address 10.16.149.62/16
	OS10(conf-if-ma-1/1/1)# no shutdown
	OS10(conf-if-ma-1/1/1)# do commit
	OS10(conf-if-ma-1/1/1)# exit

SSH is enabled in OS10 by default.

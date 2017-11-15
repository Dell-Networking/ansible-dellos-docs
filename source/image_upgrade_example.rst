########################################################################## 
Use Ansible to install or upgrade devices running Dell EMC Networking OS10
##########################################################################

This example explains how to use Ansible to install or upgrade the software image on a device running Dell EMC Networking OS10. The example playbook uses the *dellos-image-upgrade* role to upgrade or install an OS10 image on a specified switch. Before using Ansible to install the software image, you must download the software image via FTP/TFTP/SCP/HTTPDS, then specify the path to the image in the playbook. 

The *dellos-image-upgrade* role uses the ``dellos10_command`` to install or upgrade the switch, then and ``wait_for`` is used to identify the progress of the upgrade operation. Validation of the upgrade operation is handled using the ``dellos10_facts`` module.

Create simple Ansible playbook
******************************

#. Create an inventory file called *inventory.yaml*, then specify the device IP address.

::

	spine1 ansible_host=2.2.2.1 ansible_net_os_name="dellos10"

	[spine]
	spine1

	[datacenter:children]
	spine
	
#. Create a host variable file called *host_vars/spine1.yaml* then define the host, credentials, and transport.
    
:: 
    
    hostname: spine1
    provider:
      host: "{{ hostname }}"
      username: xxxxx
      password: xxxxx
      authorize: yes
      auth_pass: xxxxx  
    dellos_image_upgrade:
      operation_type: install
      software_image_url: tftp://1.1.1.1/PKGS_OS10-Enterprise-10.2.9999E.5790-installer-x86_64.bin
      software_version: 10.2.9999E
	  
#. Create a playbook called *datacenter.yaml*.

:: 

	---
	- hosts: datacenter
	  gather_facts: no
	  connection: local
	  roles:		
		- Dell-Networking.dellos-image-upgrade

#. Execute the playbook.

::

  ansible-playbook -i inventory.yaml datacenter.yaml

############# 
Release notes
#############

This information contains the release notes for Dell EMC Ansible support.

Release 3.0.0
*************

This release introduces new roles.

- ``dellos-copy-config``
- ``dellos-flow-monitor``
- ``dellos-image-upgrade``
- ``dellos-ntp``
- ``dellos-qos``
- ``dellos-route-map``

Release 2.0.0
*************

This release introduces new roles.

- ``dellos-aaa``
- ``dellos-acl``
- ``dellos-dcb``
- ``dellos-dns``
- ``dellos-ecmp``
- ``dellos-lldp``
- ``dellos-prefix-list``
- ``dellos-sflow``
- ``dellos-vlt``
- ``dellos-vrf``
- ``dellos-vrrp``
- ``dellos-snmp`` *
- ``dellos-users`` *
- ``dellos-logging`` *
	
.. note:: Roles with an asterisk (*) are part of dellos-system role in version 1.0.0.
	
Release 1.0.0
*************

This release introduces initial Ansible support for Dell EMC OS6, OS9, and OS10.

- New modules:
   
    - dellos6_command
    - dellos6_config
    - dellos6_facts
    - dellos9_command
    - dellos9_config
    - dellos9_facts
    - dellos10_command
    - dellos10_config
    - dellos10_facts

- New roles:

     - ``dellos-bgp``
     - ``dellos-interface``
     - ``dellos-lag``
     - ``dellos-system``
     - ``dellos-vlan``
     - ``dellos-xstp``

- Known issues:
     
     - dellos9_command Ansible hangs after reload command issued to remote device (see `Issue 5462 <https://github.com/ansible/ansible-modules-core/issues/5462>`_)
     - dellos9_command confirm prompt timeout (see `Issue 5534 <https://github.com/ansible/ansible-modules-core/issues/5534>`_)

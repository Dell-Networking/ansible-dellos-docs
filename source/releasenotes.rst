
==============
Release Notes
==============

Release Notes for Dell EMC Networking Ansible support.

Release Version 1.0.0
----------------------

This release introduces:

- Initial Ansible support for Dell EMC Networking OS6 / OS9 / OS10.

- New Modules:
   
    - dellos6_command
    - dellos6_config
    - dellos6_facts
    - dellos9_command
    - dellos9_config
    - dellos9_facts
    - dellos10_command
    - dellos10_config
    - dellos10_facts

- New Roles:

     - dellos-bgp
     - dellos-interface
     - dellos-lag
     - dellos-system
     - dellos-vlan
     - dellos-xstp

- Known Issues:
     
     - dellos9_command ansible hangs after reload command issued to remote device - See `Issue 5462 <https://github.com/ansible/ansible-modules-core/issues/5462>`_.
     - dellos9_command confirm prompt timeout -- See `Issue 5534 <https://github.com/ansible/ansible-modules-core/issues/5534>`_.

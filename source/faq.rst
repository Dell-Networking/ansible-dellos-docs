##########################
Frequently asked questions
##########################

You can easily find answers to commonly asked questions about Dell EMC Networking Ansible modules and roles.

Q: Which version of Ansible supports Dell EMC Networking Ansible modules?

A: Ansible 2.2 and later.

Q: What are the minimum OS versions for Ansible support?

A: OS version 6.3.1 and above; OS version 9.10.0.1P13 and above; OS version 10.2 and later.

Q: What do the Dell EMC Networking Ansible roles provide?

A: The roles are a package of multiple Dell EMC Networking OS features which are provided for easy installation, configuration, and packaging. They currently contain configuration for system, interface, VLAN, LAG, BGP, and xSTP. 

Q: Do Dell EMC Networking Ansible roles work with Ansible Tower?

A: Yes, these roles work with Ansible Tower for management.

Q: Is there dnosX_template module support for OS6/OS9/OS10?

A: No. Ansible has deprecated support for the template module, replacing it with the config module (see `Deprecations <https://github.com/ansible/ansible/blob/devel/CHANGELOG.md#deprecations>`_).

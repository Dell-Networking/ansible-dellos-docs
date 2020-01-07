##########################
Frequently asked questions
##########################

You can easily find answers to commonly asked questions about Dell EMC Ansible modules and roles.

**Which version of Ansible supports Dell EMC Ansible modules?**

Ansible 2.2 and later.

**What are the minimum OS versions for Ansible support?**

OS version 6.3.1 and above; OS version 9.10.0.1P13 and above; OS version 10.2 and later.

**What do the Dell EMC Ansible roles provide?**

The roles are a package of multiple Dell EMC OS features which are provided for easy installation, configuration, and packaging. They currently contain configuration for system, interface, VLAN, LAG, BGP, and xSTP. 

**Do Dell EMC Ansible roles work with Ansible Tower?**

Yes, these roles work with Ansible Tower for management.

**Is there dnosX_template module support for OS6/OS9/OS10?**

No. Ansible has deprecated support for the template module, replacing it with the config module (see `Deprecations <https://github.com/ansible/ansible/blob/devel/CHANGELOG.md#deprecations>`_).

=================================
Dell EMC Networking Ansible Roles
=================================

The Dell EMC Networking Ansible roles facilitate the provisioning of devices running Dell EMC Networking Operating Systems. 
These roles are abstracted for OS6, OS9, and OS10. The following roles are currently available:


BGP Role
-----------

The `dellos-bgp <https://galaxy.ansible.com/Dell-Networking/dellos-bgp/>`_ role facilitates the configuration of Border Gateway Protocol (BGP) attributes. It supports the configuration of router ID, networks, neighbors, and maximum path.


Interface Role
---------------

The `dellos-interface <https://galaxy.ansible.com/Dell-Networking/dellos-interface/>`_ role facilitates the configuration of interface attributes. It supports the configuration of administrative state, description, MTU, IP address, IP helper, and port mode. 


LAG Role
----------

The `dellos-lag <https://galaxy.ansible.com/Dell-Networking/dellos-lag/>`_ role facilitates the configuration of Link Aggregation Group (LAG) attributes. It supports the creation and deletion of a LAG and its member ports. It also supports the configuration of type (static/dynamic), hash scheme, and minimum required link.

System Role
-------------

The `dellos-system <https://galaxy.ansible.com/Dell-Networking/dellos-system/>`_ role facilitates the configuration of global system attributes. It supports the configuration of hostname, SNMP server, NTP server, logging servers, management route, and CLI users.

VLAN Role
----------

The `dellos-vlan <https://galaxy.ansible.com/Dell-Networking/dellos-vlan/>`_ role facilitates configuring virtual LAN (VLAN) attributes. It supports the creation and deletion of a VLAN and its member ports.

xSTP Role
------------

The `dellos-xstp <https://galaxy.ansible.com/Dell-Networking/dellos-xstp/>`_ role facilitates the configuration of xSTP attributes. It supports multiple version of Spanning Tree Protocol (STP): Rapid Spanning Tree (RSTP), Rapid Per-VLAN Spanning Tree (Rapid PVST+), Multiple Spanning Tree (MST), and Per-VLAN Spanning Tree (PVST). It supports the configuration of bridge priority, enabling and disabling spanning tree, creating and deleting instances, and mapping virtual LANs (VLANs) to instances. 


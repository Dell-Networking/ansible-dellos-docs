=================================
Dell EMC Networking Ansible Roles
=================================

The Dell EMC Networking Ansible roles facilitate the provisioning of devices running Dell EMC Networking Operating Systems. 
The following roles are currently available:

AAA Role
---------

The `dellos-aaa <https://galaxy.ansible.com/Dell-Networking/dellos-aaa/>`_ role facilitates the configuration of Authentication Authorization Acccounting (AAA). It supports the configuration of TACACS and RADIUS server and AAA

Abstracted for ``OS9``

ACL Role
---------

The `dellos-acl <https://galaxy.ansible.com/Dell-Networking/dellos-acl/>`_ role facilitates the configuration of an access control list (ACL). It supports the configuration of different types of ACLs (standard and extended) for both IPv4 and IPv6, and assigns the access-class to the line terminals

Abstracted for ``OS9``

BGP Role
-----------

The `dellos-bgp <https://galaxy.ansible.com/Dell-Networking/dellos-bgp/>`_ role facilitates the configuration of Border Gateway Protocol (BGP) attributes. It supports the configuration of router ID, networks, neighbors, and maximum path.

Abstracted for ``OS6`` ``OS9`` ``OS10``

DCB Role
---------

The `dellos-dcb <https://galaxy.ansible.com/Dell-Networking/dellos-dcb/>`_ role facilitates the configuration of Data Center Bridging (DCB). It supports the configuration of DCB map and DCB buffer and assigns them to interfaces

Abstracted for ``OS9``

DNS Role
---------

The `dellos-dns <https://galaxy.ansible.com/Dell-Networking/dellos-dns/>`_ role facilitates the configuration of Domian name service(DNS)

Abstracted for ``OS9``

ECMP Role
---------

The `dellos-ecmp <https://galaxy.ansible.com/Dell-Networking/dellos-ecmp/>`_ role facilitates the configuration of Equal Cost Multi Path (ECMP). It supports the configuration of ECMP for IPv4

Abstracted for ``OS9``

Interface Role
---------------

The `dellos-interface <https://galaxy.ansible.com/Dell-Networking/dellos-interface/>`_ role facilitates the configuration of interface attributes. It supports the configuration of administrative state, description, MTU, IP address, IP helper, and port mode. 

Abstracted for ``OS6`` ``OS9`` ``OS10``

LAG Role
----------

The `dellos-lag <https://galaxy.ansible.com/Dell-Networking/dellos-lag/>`_ role facilitates the configuration of Link Aggregation Group (LAG) attributes. It supports the creation and deletion of a LAG and its member ports. It also supports the configuration of type (static/dynamic), hash scheme, and minimum required link.

Abstracted for ``OS6`` ``OS9`` ``OS10``

LLDP Role
---------

The `dellos-lldp <https://galaxy.ansible.com/Dell-Networking/dellos-lldp/>`_ role facilitates the configuration of Link Layer Discovery Protocol(LLDP) attributes at global and interface level. It supports the configuration of hello, mode, multiplier, advertise tlvs, management interface, fcoe, iscsi at global and interface level

Abstracted for ``OS9`` ``OS10``

Logging Role
---------------

The `dellos-logging <https://galaxy.ansible.com/Dell-Networking/dellos-logging/>`_ role facilitates the configuration of global logging attributes. It supports the configuration of logging servers. 

Abstracted for ``OS6`` ``OS9`` ``OS10``

Prefix list Role
-----------------

The `dellos-prefix-list <https://galaxy.ansible.com/Dell-Networking/dellos-prefix-list/>`_ role facilitates the configuration of a prefix list. It supports the configuration of ip prefix-list, and assigns the prefix-list to the line terminals

Abstracted for ``OS9``

sFlow Role
---------------

The `dellos-sflow <https://galaxy.ansible.com/Dell-Networking/dellos-sflow/>`_ role facilitates the configuration of global and interface level sflow attributes. It supports the configuration of sflow collectors at global level. Enabling and disabling of sflow and specification of sflow polling-interval, sample-rate, max-datagram size , etc; are supported at interface and global level

Abstracted for ``OS9``

SNMP Role
---------------

The `dellos-snmp <https://galaxy.ansible.com/Dell-Networking/dellos-snmp/>`_ role facilitates the configuration of global snmp attributes. It supports the configuration of SNMP server attributes like users, group, community, location, traps, etc;

Abstracted for ``OS9`` ``OS10``

System Role
-------------

The `dellos-system <https://galaxy.ansible.com/Dell-Networking/dellos-system/>`_ role facilitates the configuration of global system attributes. It specifically enables configuration of hostname, NTP server and enable password for all three dellos. In addition to this dellos9 supports the configuration of management route, hash alogrithm, clock, line terminal, banner and reload type.

Abstracted for ``OS6`` ``OS9`` ``OS10``

Users Role
---------------

The `dellos-users <https://galaxy.ansible.com/Dell-Networking/dellos-users/>`_ role facilitates the configuration of global system user attributes. It supports the configuration of CLI users.

Abstracted for ``OS6`` ``OS9`` ``OS10``

VLAN Role
----------

The `dellos-vlan <https://galaxy.ansible.com/Dell-Networking/dellos-vlan/>`_ role facilitates configuring virtual LAN (VLAN) attributes. It supports the creation and deletion of a VLAN and its member ports.

Abstracted for ``OS6`` ``OS9`` ``OS10``

VLT Role
---------------

The `dellos-vlt <https://galaxy.ansible.com/Dell-Networking/dellos-vlt/>`_ role facilitates the configuration of the basics of Virtual Link Trunking (VLT) to provide a loop-free topology.

Abstracted for ``OS9`` ``OS10``

VRF Role
---------------

The `dellos-vrf <https://galaxy.ansible.com/Dell-Networking/dellos-vrf/>`_ role facilitates to configure the basics of virtual routing and forwarding (VRF) that helps in the partition of physical routers to multiple virtual routers

Abstracted for ``OS9``

VRRP Role
---------------

The `dellos-vrrp <https://galaxy.ansible.com/Dell-Networking/dellos-vrrp/>`_ role facilitates configuring Virtual Router Redundancy Protocol (VRRP) attributes. It supports the creation of vrrp groups for interfaces and setting the vrrp group attributes

Abstracted for ``OS6`` ``OS9`` ``OS10``

xSTP Role
------------

The `dellos-xstp <https://galaxy.ansible.com/Dell-Networking/dellos-xstp/>`_ role ffacilitates the configuration of xSTP attributes. It supports multiple version of Spanning Tree Protocol (STP): Rapid Spanning Tree (RSTP), Multiple Spanning Tree (MST), and Per-VLAN Spanning Tree (PVST). It supports the configuration of bridge priority, enabling and disabling spanning tree, creating and deleting instances, and mapping virtual LAN (VLAN) to instances

Abstracted for ``OS6`` ``OS9`` ``OS10``
################################# 
Dell EMC Networking Ansible roles
#################################

The Dell EMC Networking Ansible roles facilitate device provisioning running Dell EMC Networking OS6, OS9, or OS10. This information describes the Dell EMC Networking Ansible roles.

AAA role
--------

The `dellos-aaa <https://galaxy.ansible.com/Dell-Networking/dellos-aaa/>`_ role facilitates the configuration of authentication authorization acccounting (AAA), and supports the configuration of TACACS and RADIUS server and AAA.

Abstracted for ``OS6`` ``OS9`` ``OS10``

ACL role
--------

The `dellos-acl <https://galaxy.ansible.com/Dell-Networking/dellos-acl/>`_ role facilitates the configuration of an access control list (ACL). It supports the configuration of different types of ACLs (standard and extended) for both IPv4 and IPv6, and assigns the access-class to line terminals.

Abstracted for ``OS6`` ``OS9``

BGP role
--------

The `dellos-bgp <https://galaxy.ansible.com/Dell-Networking/dellos-bgp/>`_ role facilitates the configuration of border gateway protocol (BGP) attributes, and supports router ID, networks, neighbors, and maximum path configurations.

Abstracted for ``OS6`` ``OS9`` ``OS10``


Copy-config role
----------------

The `dellos-copy-config <https://galaxy.ansible.com/Dell-Networking/dellos-copy-config/>`_ role pushes the backup running configuration into a device. This role merges the configuration in the template file with the running configuration of the Dell EMC Networking device.

Abstracted for ``OS6`` ``OS9`` ``OS10``

DCB role
--------

The `dellos-dcb <https://galaxy.ansible.com/Dell-Networking/dellos-dcb/>`_ role facilitates the configuration of data center bridging (DCB), supports the configuration of DCB map and DCB buffer and assigns them to interfaces.

Abstracted for ``OS9``

DNS role
--------

The `dellos-dns <https://galaxy.ansible.com/Dell-Networking/dellos-dns/>`_ role facilitates the configuration of domain name service (DNS).

Abstracted for ``OS9``

ECMP role
---------

The `dellos-ecmp <https://galaxy.ansible.com/Dell-Networking/dellos-ecmp/>`_ role facilitates the configuration of equal cost multi-path (ECMP). It supports the configuration of ECMP for IPv4.

Abstracted for ``OS9``

Flow-monitor role
-----------------

The `dellos-flow-monitor <https://galaxy.ansible.com/Dell-Networking/dellos-flow-monitor/>`_ role facilitates the configuration of ACL flow-based monitoring attributes. Flow-based mirroring is a mirroring session in which traffic matches specified policies that are mirrored to a destination port. Port-based mirroring maintains a database that contains all monitoring sessions (including port monitor sessions).

Abstracted for ``OS10``

Image-upgrade role
------------------

The `dellos-image-upgrade <https://galaxy.ansible.com/Dell-Networking/dellos-image-upgrade/>`_ role facilitates upgrades or installation of an OS10 software image.

Abstracted for ``OS6`` ``OS9`` ``OS10``


Interface role
--------------

The `dellos-interface <https://galaxy.ansible.com/Dell-Networking/dellos-interface/>`_ role facilitates the configuration of interface attributes. It supports the configuration of administrative state, description, MTU, IP address, IP helper, and port mode. 

Abstracted for ``OS10``

LAG role
--------

The `dellos-lag <https://galaxy.ansible.com/Dell-Networking/dellos-lag/>`_ role facilitates the configuration of link aggregation group (LAG) attributes. This role supports the creation and deletion of a LAG and its member ports, and supports the configuration of type (static/dynamic), hash scheme, and minimum required link.

Abstracted for ``OS6`` ``OS9`` ``OS10``

LLDP role
---------

The `dellos-lldp <https://galaxy.ansible.com/Dell-Networking/dellos-lldp/>`_ role facilitates the configuration of link layer discovery protocol (LLDP) attributes at global and interface level. This role supports the configuration of hello, mode, multiplier, advertise tlvs, management interface, fcoe, iscsi at global and interface levels.

Abstracted for ``OS6`` ``OS9`` ``OS10``

Logging role
------------

The `dellos-logging <https://galaxy.ansible.com/Dell-Networking/dellos-logging/>`_ role facilitates the configuration of global logging attributes, and supports the configuration of logging servers. 

Abstracted for ``OS6`` ``OS9`` ``OS10``

NTP role
--------

The `dellos-ntp <https://galaxy.ansible.com/Dell-Networking/dellos-ntp/>`_ role facilitates the configuration of network time protocol attributes.

Abstracted for ``OS6`` ``OS9`` ``OS10``

Prefix-list role
----------------

The `dellos-prefix-list <https://galaxy.ansible.com/Dell-Networking/dellos-prefix-list/>`_ role facilitates the configuration of a prefix-list, supports the configuration of IP prefix-list, and assigns the prefix-list to line terminals.

Abstracted for ``OS9``

QoS role
--------

The `dellos-qos <https://galaxy.ansible.com/Dell-Networking/dellos-qos/>`_ role facilitates the configuration of quality of service attributes including policy-map and class-map.

Abstracted for ``OS6`` ``OS10``

Route-map role
--------------

The `dellos-route-map <https://galaxy.ansible.com/Dell-Networking/dellos-route-map/>`_ role facilitates the configuration of route-map attributes.

Abstracted for ``OS10``

sFlow role
----------

The `dellos-sflow <https://galaxy.ansible.com/Dell-Networking/dellos-sflow/>`_ role facilitates the configuration of global and interface-level sflow attributes. This role supports the configuration of sflow collectors at the global level, enabling and disabling of sflow and specification of sflow polling-interval, sample-rate, max-datagram sizs, and so on are supported at interface and global levels.

Abstracted for ``OS9``

SNMP role
---------

The `dellos-snmp <https://galaxy.ansible.com/Dell-Networking/dellos-snmp/>`_ role facilitates the configuration of global snmp attributes. It supports the configuration of SNMP server attributes like users, group, community, location, traps, and so on.

Abstracted for ``OS9`` ``OS10``

System role
-----------

The `dellos-system <https://galaxy.ansible.com/Dell-Networking/dellos-system/>`_ role facilitates the configuration of global system attributes. This role specifically enables configuration of hostname, NTP server, and enables the password for dellos6, dellos9, and dellos10. dellos9 supports the configuration of the management route, hash alogrithm, clock, line terminal, banner and reload type.

Abstracted for ``OS6`` ``OS9`` ``OS10``

Users role
----------

The `dellos-users <https://galaxy.ansible.com/Dell-Networking/dellos-users/>`_ role facilitates the configuration of global system user attributes. This role supports the configuration of CLI users.

Abstracted for ``OS6`` ``OS9`` ``OS10``

VLAN role
---------

The `dellos-vlan <https://galaxy.ansible.com/Dell-Networking/dellos-vlan/>`_ role facilitates configuring virtual LAN (VLAN) attributes. This role supports the creation and deletion of a VLAN and its member ports.

Abstracted for ``OS6`` ``OS9`` ``OS10``

VLT role
--------

The `dellos-vlt <https://galaxy.ansible.com/Dell-Networking/dellos-vlt/>`_ role facilitates the configuration of the basics of virtual link trunking (VLT) to provide a loop-free topology.

Abstracted for ``OS9`` ``OS10``

VRF role
--------

The `dellos-vrf <https://galaxy.ansible.com/Dell-Networking/dellos-vrf/>`_ role facilitates the configuration of basic virtual routing and forwarding (VRF) that helps in the partition of physical routers to multiple virtual routers.

Abstracted for ``OS9``

VRRP role
---------

The `dellos-vrrp <https://galaxy.ansible.com/Dell-Networking/dellos-vrrp/>`_ role facilitates configuration of virtual router redundancy protocol (VRRP) attributes. This role supports the creation of vrrp groups for interfaces, and setting the vrrp group attributes.

Abstracted for ``OS6`` ``OS9`` ``OS10``

xSTP role
---------

The `dellos-xstp <https://galaxy.ansible.com/Dell-Networking/dellos-xstp/>`_ role facilitates the configuration of xSTP attributes. This role supports multiple version of spanning-tree protocol (STP), rapid spanning-tree (RSTP) protocol, multiple spanning-tree (MST), and per-VLAN spanning-tree (PVST). This role supports the configuration of bridge priority, enabling and disabling spanning-tree, creating and deleting instances, and mapping virtual LAN (VLAN) to instances.

Abstracted for ``OS6`` ``OS9`` ``OS10``

VXLAN role
----------

The `dellos_vxlan <https://galaxy.ansible.com/Dell-Networking/dellos_vxlan/>`_ role facilitates the configuration of  virtual extensible LAN (VXLAN)   attributes. It supports the configuration of Virtual Networks, Ethernet Virtual Private Network (evpn) and Network Virtualization Edge (nve).

Abstracted for ``OS10``

BFD role
--------

The `dellos_bfd <https://galaxy.ansible.com/Dell-Networking/dellos_bfd/>`_ This role facilitates the configuration of BFD global attributes, and is abstracted for dellos10. It specifically enables configuration of bfd interval , min_rx, multiplier and role.

Abstracted for ``OS10``

TEMPLATE role
-------------

The `dellos_template <https://galaxy.ansible.com/Dell-Networking/dellos_template/>`_ This role facilitates the TEXTFSM parsing engine. TextFSM is a template based state machine . It takes the raw string input from the CLI of network devices  dellos10 , run them through a TEXTFSM template and return structured text in the form of a Python dictionary.

Abstracted for ``OS10``

UPLINK role
-----------

The `dellos_uplink <https://galaxy.ansible.com/Dell-Networking/dellos_uplink/>`_ This role facilitates the configuration of uplink attributes, and is abstracted for dellos10. It specifically enables configuration of  association between upstream and downstream interfaces known as uplink-state group.

Abstracted for ``OS10``

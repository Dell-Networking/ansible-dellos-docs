==================================================================================
Provision SMART FABRIC SERVICES using Dell EMC Networking Ansible modules example
==================================================================================
This example describes how to use Ansible to build a SMART FABRIC CLUSTER and provision the SMART FABRIC SERVICES with Dell EMC Networking OS10 switches.

The sample topology is build with one spine and two leafs connected as mesh. BGP is running between the leafs. VLTi is configured between leafs. 

It also describes to facilitates the configuration of smart fabric and provisioning its attributes through RESTful APIs. 


Creating a Ansible Playbook for SMART FABRIC Setup
---------------------------------------------------

**Step 1**

Create an inventory file called ``hosts.yaml`` and specify the device IP address and python_interpreter:


::

  leaf1 ansible_host=10.11.180.9 ansible_python_interpreter=/usr/bin/python3 
  leaf2 ansible_host=10.11.180.8 ansible_python_interpreter=/usr/bin/python3 
  spine1 ansible_host=10.11.180.10 ansible_python_interpreter=/usr/bin/python3 
  
  [Spine]
  spine1

  [Leaf]
  leaf1
  leaf2

  [LeafAndSpineSwitch:children]
  Spine
  Leaf



**Step 2**

Create a host variable file called ``host_vars/leaf1.yaml``, then define the host, credentials and sfs fabric cluster setup input:

:: 
    
    ---
    ansible_host: 10.11.180.8
    ansible_network_os: dellos10
    ansible_user: XXXXX
    ansible_password: XXXXX

    sfs_setup:
      - service_enable: True
        role: LEAF
        icl_ports: ["ethernet1/1/5","ethernet1/1/6"]



Create a host variable file called ``host_vars/leaf2.yaml``, then define the host, credentials and sfs fabric cluster setup input:

:: 
    
    ---
    ansible_host: 10.11.180.9
    ansible_network_os: dellos10
    ansible_user: XXXXX
    ansible_password: XXXXX

    sfs_setup:
      - service_enable: True
        role: LEAF
        icl_ports: ["ethernet1/1/5","ethernet1/1/6"]


Create a host variable file called ``host_vars/spine1.yaml``, then define the host, credentials and sfs fabric cluster setup input:

:: 
    
    ---
    ansible_host: 10.11.180.10
    ansible_network_os: dellos10
    ansible_user: XXXXX
    ansible_password: XXXXX

    sfs_setup:
      - service_enable: True
        role: SPINE
        icl_ports: ["ethernet1/1/5","ethernet1/1/6"]


**Step 3**

Create a playbook called ``sfs_setup.yml``:

:: 

    ---
    - name: SFS setup
      hosts: LeafAndSpineSwitch
      gather_facts: False
      connection: local
      roles:
        - sfs-setup


**Step 4**

Execute the playbook:

``ansible-playbook -i hosts.yaml sfs_setup.yml``


Creating an Ansible Playbook for SMART FABRIC API Services 
-----------------------------------------------------------

**Step 1**

Use the same inventory ``hosts.yaml`` for provisioning once the SFS setup is ready.

Create a group variable file called ``group_vars/sfs.all.yaml``, then define the  Smart Fabric Service input model:

:: 

    ---
    sfs_port_breakout:
      - target_port: GGVQG02:ethernet1/1/22
        breakout_type: 4X10GE
      - target_port: GGVQG02:ethernet1/1/23
        breakout_type: 1X100GE
      - target_port: GGVQG02:ethernet1/1/24
        breakout_type: 1X40GE
    
    sfs_port_property:
      - target_port: GGVQG02:ethernet1/1/25
        port_description: "Description for ethernet1/1/25"
        port_name: ethernet1/1/25
        admin_status: Enabled
        mtu: 1564
        auto_neg: Enabled
        configured_speed: 1024
      - target_port: GGVQG02:ethernet1/1/26
        port_description: "Description for ethernet1/1/26"
        port_name: ethernet1/1/26
        admin_status: Enabled
        mtu: 2564
        auto_neg: Enabled
        configured_speed: 1024

    sfs_uplinks:
      - uplink_name: Leaf-1-port-21
        uplink_description: "Leaf-1-port-21"
        uplink_id: "Leaf-1-port-21"
        media_type: Ethernet
        node: GGVQG02
        configuration_interfaces:
          - "ethernet1/1/21"
          - "ethernet1/1/22"
        tagged_networks:
          - "Client_Control_Network"
        untagged_network: "Client_Control_Network"
        lag_type: "Static"
        uplink_type: "Normal"
        state: present
      - uplink_name: Leaf-1-port-25
        uplink_description: "Leaf-1-port-25"
        uplink_id: "Leaf-1-port-25"
        media_type: Ethernet
        node: GGVQG02
        configuration_interfaces:
          - "ethernet1/1/25"
          - "ethernet1/1/26"
        tagged_networks:
          - "Client_Management_Network"
        untagged_network: "Client_Control_Network"
        lag_type: "Dynamic"
        uplink_type: "JumpBox"
        state: present

    sfs_route_policies:
      - policy_id: policyBGP100
        policy_name: policyBGP100name
        policy_description: policyBGP100desc
        address_family_type: ipv4
        remote_address: "192.168.2.6"
        remote_loopback_address: "192.168.2.8"
        remote_as: 65001
        policy_type: 1
        sender_side_loop_detection: 1
        route_filter_enable: 1
        state: present
      - policy_id: policyBGP101
        policy_name: policyBGP101name
        policy_description: policyBGP101desc
        address_family_type: ipv4
        remote_address: "192.168.2.2"
        remote_loopback_address: "192.168.2.4"
        remote_as: 65001
        policy_type: 1
        sender_side_loop_detection: 1
        route_filter_enable: 1
        state: present
      - policy_id: policyStaticCRoute1
        policy_name: policyStaticRoute1name
        policy_description: policyStaticRoute1desc
        policy_type: 2
        ipv4_address_prefix: "99.99.99.0"
        ipv4_prefix_len: 24
        ipv4_nexthop_ip: "99.99.99.2"
        state: present

    sfs_node_policy_mapping:
      - node: "GGVQG02"
        policy_list:
          - policyBGP100
          - policyBGP101
          - policyStaticCRoute1
        state: present

    sfs_networks:
      - name: Leaf-test-sfs-VXLAN
        id: Leaf-test-sfs-VXLAN
        vlan_min: 650
        vlan_max: 650
        qos_priority: Silver
        type: VXLAN
        description: "SFS Network Create Test From Ansible"
        address_family: inet
        gateway_ip_address: ["192.168.1.3"]
        helper_address: ["10.10.10.10","11.11.11.11"]
        ip_address_list: ["192.168.1.2","192.168.1.4"]
        prefix_length: 31
        route_map: "routemap1"
        virtual_network: esxi_build650
        state: present
      - name: Leaf-test-sfs-VXLAN
        id: Leaf-test-GeneralPurpose
        vlan_min: 750
        vlan_max: 750
        qos_priority: Gold
        type: GeneralPurpose
        description: "SFS Network Create Test From Ansible"
        address_family: inet
        virtual_network: vn750
        state: present
      - name: Leaf-test-sfs1-network-l3
        id: Leaf-test-sfs1-network-l3
        vlan_min: 550
        vlan_max: 550
        qos_priority: Bronze
        type: L3
        description: "SFS L3 Network Create Test From Ansible"
        address_family: inet
        gateway_ip_address: ["192.168.1.3"]
        helper_address: ["10.10.10.10","11.11.11.11"]
        ip_address_list: ["192.168.1.2","192.168.1.4"]
        prefix_length: 31
        route_map: "routemap1"
        state: present
      - name: Leaf-test-sfs1-network-l3-routed
        id: Leaf-test-sfs1-network-l3-routed
        qos_priority: Bronze
        type: L3_ROUTED
        description: "SFS L3-ROUTED Network Create Test From Ansible"
        address_family: inet
        gateway_ip_address: ["192.168.1.3"]
        helper_address: ["10.10.10.10","15.15.15.15"]
        ip_address_list: ["192.168.1.2","192.168.1.4","192.168.1.6"]
        prefix_length: 31
        route_map: "routemap2"
        state: present

    sfs_virtual_networks:
      - virtual_network_name: "vnet604"
        virtual_network_description: "vnet604 Create"
        virtual_network_type: "General Purpose (Bronze)"
        vxlanvni: 1604
        vltvlanid: 604
        gateway_ip_address: "172.17.105.1"
        gateway_mac_address: "00:11:12:01:23:36"
        prefix_length: 24
        address_family: "inet"
        ip_address_list:
          - "172.17.105.2"
          - "172.17.105.3"
        helper_address: ["2.2.2.2","3.3.3.3"]
        state: present
      - virtual_network_name: "vnet605"
        virtual_network_description: "vnet605 Create"
        virtual_network_type: "Cluster Interconnect"
        vxlanvni: 1605
        vltvlanid: 605
        gateway_ip_address: "172.17.105.1"
        gateway_mac_address: "00:11:12:01:23:36"
        prefix_length: 24
        address_family: "inet"
        ip_address_list:
          - "172.17.105.10"
          - "172.17.105.11"
        helper_address: ["10.10.10.10","11.11.11.11"]
        state: present

    sfs_server_profiles:
      - server_id: server-1
        bonding_technology: Static
        interface_profiles:
          - id: ethernet1/1/43
            tagged_networks:
              - Client_Control_Network
            nic_bonded: True
            state: present
          - id: ethernet1/1/44
            tagged_networks:
              - Client_Control_Network
            nic_bonded: True
            state: present
        state: present
      - server_id: server-2
        bonding_technology: LACP
        interface_profiles:
          - id: ethernet1/1/33
            tagged_networks:
              - Client_Management_Network
            nic_bonded: True
            state: present
          - id: ethernet1/1/34
            tagged_networks:
              - Client_Management_Network
            nic_bonded: True
            state: present
        state: present

    sfs_fabric_property:
      - leaf_asn: 65011
        spine_asn: 65012
        private_subnet_prefix: "172.16.0.0"
        private_prefix_len: 16
        global_subnet_prefix: "172.30.0.0"
        global_prefix_len: 16
        client_control_vlan: 3939
        client_management_vlan: 4091

    sfs_fabric_reboot:
      - node: GGVQG02
        state: absent




**Step 2**

Create a playbook called ``sfs_provision.yml``:


:: 

    ---
    - name: SFS Provisioning
      hosts: localhost
      gather_facts: False
      connection: local
      pre_tasks:
        - name: Include Variables for sfs provisioning
          include_vars:
            file: group_vars/sfs.all.yaml
      roles:
        - sfs-network
        - sfs-virtual-network
        - sfs-uplink
        - sfs-route-policy
        - sfs-node-policy-mapping
        - sfs-port-breakout
        - sfs-port-properties
        - sfs-validation-errors
        - sfs-server-profile


**Step 3**

Execute the playbook:

``ansible-playbook -i hosts.yaml sfs_provision.yml``

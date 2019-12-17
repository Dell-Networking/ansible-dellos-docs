=======================================================================
Provision CLOS fabric using Dell EMC Ansible modules example
=======================================================================

This example describes how to use Ansible to build a CLOS fabric with Dell EMC SmartFabric OS10 switches. The sample topology is a two-tier CLOS fabric with two spines and four leafs connected as mesh. eBGP is running between the two tiers. All switches in spine have the same AS number, and each leaf switch has a unique AS number. All AS numbers used are private. 

For application load-balancing purposes, the same prefix is advertised from multiple leaf switches and uses *BGP multipath relax* feature.


.. figure:: ./_static/topo.png
   :scale: 50 %
   :alt: map to buried treasure

Create a simple Ansible playbook
----------------------------------

**Step 1**

Create an inventory file called ``inventory.yaml``, then specify the device IP address.


::

	spine1 ansible_host=10.11.182.25
	spine2 ansible_host=10.11.182.26 
	leaf1 ansible_host=10.11.182.27 
	leaf2 ansible_host=10.11.182.28 
	leaf3 ansible_host=10.11.182.29 
	leaf4 ansible_host=10.11.182.30

	[spine]
	spine1
	spine2

	[leaf]
	leaf1
	leaf2
	leaf3
	leaf4

	[datacenter:children]
	spine
	leaf


**Step 2**

Create a group variable file called ``group_vars/all``, then define credentials and SNMP variables.

::

     ansible_ssh_user: xxxxx
     ansible_ssh_pass: xxxxx
     ansible_network_os: dellos10

     dellos_snmp:
       snmp_community:
         - name: public
           access_mode: ro
           state: present

**Step 3**

Create a group variable file called ``group_vars/spine.yaml``, then define credentials, hostname, and BGP neighbors of spine group.

::

     ansible_ssh_user: xxxxx
     ansible_ssh_pass: xxxxx
     ansible_network_os: dellos10

     dellos_system:
       hostname: "{{ spine_hostname }}"

     dellos_bgp:
        asn: 64901
        router_id: "{{ bgp_router_id }}"
        best_path:
           as_path: multipath-relax
           as_path_state: present
           med:
            - attribute: missing-as-worst
              state: present
        neighbor:
          - type: ipv4
            remote_asn: "{{ bgp_neigh1_remote_asn }}"
            ip: "{{ bgp_neigh1_ip }}"
            admin: up
            state: present
          - type: ipv4
            remote_asn: "{{ bgp_neigh2_remote_asn }}"
            ip: "{{ bgp_neigh2_ip }}"
            admin: up
            state: present
          - type: ipv4
            remote_asn: "{{ bgp_neigh3_remote_asn }}"
            ip: "{{ bgp_neigh3_ip }}"
            admin: up
            state: present
          - type: ipv4
            remote_asn: "{{ bgp_neigh4_remote_asn }}"
            ip: "{{ bgp_neigh4_ip }}"
            admin: up
            state: present        
          - type: ipv6
            remote_asn: "{{ bgp_neigh5_remote_asn }}"
            ip: "{{ bgp_neigh5_ip }}"
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
            state: present
          - type: ipv6
            remote_asn: "{{ bgp_neigh6_remote_asn }}"
            ip: "{{ bgp_neigh6_ip }}"
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
            state: present
          - type: ipv6
            remote_asn: "{{ bgp_neigh7_remote_asn }}"
            ip: "{{ bgp_neigh7_ip }}"
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
            state: present
          - type: ipv6
            remote_asn: "{{ bgp_neigh8_remote_asn }}"
            ip: "{{ bgp_neigh8_ip }}"
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
        state: present
    
**Step 4**

Create a host variable file called ``host_vars/spine1.yaml``, then define the host, credentials, and transport.
    
:: 
    
    hostname: spine1
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10
    spine_hostname: "spine-1"
    
    dellos_interface:
        ethernet 1/1/1:
                desc: "Connected to leaf 1"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.1.1.1/24
                ipv6_and_mask: 2001:100:1:1::1/64
                state_ipv6: present
        ethernet 1/1/17:
                desc: "Connected to leaf 2"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.1.33.1/24
                ipv6_and_mask: 2001:100:1:21::1/64
                state_ipv6: present
        ethernet 1/1/25:
                desc: "Connected to leaf 3" 
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.1.17.1/24
                ipv6_and_mask: 2001:100:1:11::1/64
                state_ipv6: present
        ethernet 1/1/9:
                desc: "Connected to leaf 4"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.1.49.1/24
                ipv6_and_mask: 2001:100:1:31::1/64
                state_ipv6: present            

    bgp_router_id: "100.0.1.1" 
    bgp_neigh1_remote_asn: 64801
    bgp_neigh1_ip: "100.1.1.2"
    bgp_neigh2_remote_asn: 64803
    bgp_neigh2_ip: "100.1.33.2"
    bgp_neigh3_remote_asn: 64802
    bgp_neigh3_ip: "100.1.17.2"
    bgp_neigh4_remote_asn: 64804
    bgp_neigh4_ip: "100.1.49.2"
    bgp_neigh5_remote_asn: 64801
    bgp_neigh5_ip: "2001:100:1:1::2"
    bgp_neigh6_remote_asn: 64802
    bgp_neigh6_ip: "2001:100:1:11::2"
    bgp_neigh7_remote_asn: 64803
    bgp_neigh7_ip: "2001:100:1:21::2"
    bgp_neigh8_remote_asn: 64804
    bgp_neigh8_ip: "2001:100:1:31::2"


Create a host variable file called ``host_vars/spine2.yaml``, then define the host, credentials, and transport.
            
:: 

    hostname: spine2
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10
    spine_hostname: "spine-2"
    dellos_interface:
        ethernet 1/1/1:
                desc: "Connected to leaf 1" 
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.2.1.1/24
                ipv6_and_mask: 2001:100:2:1::1/64
                state_ipv6: present
        ethernet 1/1/25:
                desc: "Connected to leaf 2"  
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.2.17.1/24
                ipv6_and_mask: 2001:100:2:11::1/64
                state_ipv6: present
        ethernet 1/1/17:
                desc: "Connected to leaf 3"     
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.2.33.1/24
                ipv6_and_mask: 2001:100:2:21::1/64
                state_ipv6: present
        ethernet 1/1/9:
                desc: "Connected to leaf 4"  
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.2.49.1/24
                ipv6_and_mask: 2001:100:2:31::1/64
                state_ipv6: present
            
    bgp_router_id: "100.0.1.2"
    bgp_neigh1_remote_asn: 64801
    bgp_neigh1_ip: "100.2.1.2"
    bgp_neigh2_remote_asn: 64802
    bgp_neigh2_ip: "100.2.33.2"
    bgp_neigh3_remote_asn: 64803
    bgp_neigh3_ip: "100.2.17.2"
    bgp_neigh4_remote_asn: 64804
    bgp_neigh4_ip: "100.2.49.2"
    bgp_neigh5_remote_asn: 64801
    bgp_neigh5_ip: "2001:100:2:1::2"
    bgp_neigh6_remote_asn: 64802
    bgp_neigh6_ip: "2001:100:2:11::2"
    bgp_neigh7_remote_asn: 64803
    bgp_neigh7_ip: "2001:100:2:21::2"
    bgp_neigh8_remote_asn: 64804
    bgp_neigh8_ip: "2001:100:2:31::2"

Create a host variable file called ``host_vars/leaf1.yaml``, then define the host, credentials, and transport.

:: 

    hostname: leaf1
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10
    dellos_system:
      hash_algo:
        algo:
          - name: ecmp
            mode: crc
            state: present          
    dellos_interface:
        ethernet 1/1/1:
                desc: "Connected to Spine 1"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.1.1.2/24
                ipv6_and_mask: 2001:100:1:1::2/64
                state_ipv6: present
        ethernet 1/1/9:
                desc: "Connected to Spine 2"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.2.1.2/24
                ipv6_and_mask: 2001:100:2:1::2/64
                state_ipv6: present
    dellos_bgp:
        asn: 64801
        router_id: 100.0.2.1
        address_family_ipv4: true
        address_family_ipv6: true		
        best_path:
           as_path: multipath-relax
           as_path_state: present
           med:
            - attribute: missing-as-worst
              state: present
        neighbor:
          - type: ipv4
            remote_asn: 64901
            ip: 100.1.1.1
            admin: up
            state: present
          - type: ipv4
            remote_asn: 64901
            ip: 100.2.1.1
            admin: up
            state: present
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:1:1::1
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
            state: present
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:2:1::1
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
            state: present
        state: present

Create a host variable file called ``host_vars/leaf2.yaml``, then define the host, credentials, and transport.

:: 

    hostname: leaf2
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10
    dellos_system:
      hash_algo:
        algo:
          - name: ecmp
            mode: crc
            state: present          
    dellos_interface:
        ethernet 1/1/1:
                desc: "Connected to Spine 1"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.1.17.2/24
                ipv6_and_mask: 2001:100:1:11::2/64
                state_ipv6: present
        ethernet 1/1/9:
                desc: "Connected to Spine 2"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.2.17.2/24
                ipv6_and_mask: 2001:100:2:11::2/64
    dellos_bgp:
        asn: 64802
        router_id: 100.0.2.2
        address_family_ipv4: true
        address_family_ipv6: true		
        best_path:
           as_path: multipath-relax
           as_path_state: present
           med:
            - attribute: missing-as-worst
              state: present
        neighbor:
          - type: ipv4
            remote_asn: 64901
            ip: 100.1.18.1
            admin: up
            state: present
          - type: ipv4
            remote_asn: 64901
            ip: 100.1.17.1
            admin: up
            state: present
          - type: ipv4
            remote_asn: 64901
            ip: 100.2.17.1
            admin: up
            state: present
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:1:11::1
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
            state: present
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:2:11::1
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present          
        state: present
            
:: 

    hostname: leaf3
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10
    dellos_system:
      hash_algo:
        algo:
          - name: ecmp
            mode: crc
            state: present          
    dellos_interface:
        ethernet 1/1/1:
                desc: "Connected to Spine 1"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.1.33.2/24
                ipv6_and_mask: 2001:100:1:21::2/64
                state_ipv6: present
        ethernet 1/1/9:
                desc: "Connected to Spine 2"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.2.33.2/24
                ipv6_and_mask: 2001:100:2:21::2/64
    dellos_bgp:
        asn: 64803
        router_id: 100.0.2.3
        address_family_ipv4: true
        address_family_ipv6: true
        best_path:
           as_path: multipath-relax
           as_path_state: present
           med:
            - attribute: missing-as-worst
              state: present
        neighbor:
          - type: ipv4
            remote_asn: 64901
            ip: 100.1.33.1
            admin: up
            state: present
          - type: ipv4
            remote_asn: 64901
            ip: 100.2.33.1
            admin: up
            state: present
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:1:21::1
            admin: up
            state: present
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:1:22::1
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
            state: present
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:2:21::1
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present         
        state: present

Create a host variable file called ``host_vars/leaf4.yaml``, then define the host, credentials, and transport.

:: 

    hostname: leaf4
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10
    dellos_system:
      hash_algo:
        algo:
          - name: ecmp
            mode: crc
            state: present          
    dellos_interface:
        ethernet 1/1/5:
                desc: "Connected to Spine 1"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.1.49.2/24
                ipv6_and_mask: 2001:100:1:31::2/64
                state_ipv6: present
        ethernet 1/1/17:
                desc: "Connected to Spine 2"
                mtu: 9216
                portmode:
                admin: up
                switchport: False
                ip_and_mask: 100.2.49.2/24
                ipv6_and_mask: 2001:100:2:31::2/64
                state_ipv6: present
    dellos_bgp:
        asn: 64804
        router_id: 100.0.2.4
        address_family_ipv4: true
        address_family_ipv6: true
        best_path:
           as_path: multipath-relax
           as_path_state: present
           med:
            - attribute: missing-as-worst
              state: present
        neighbor:
          - type: ipv4
            remote_asn: 64901
            ip: 100.1.49.1
            admin: up
            state: present
          - type: ipv4
            remote_asn: 64901
            ip: 100.2.49.1
            admin: up
            state: present
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:1:31::1
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present   
            state: present    
          - type: ipv6
            remote_asn: 64901
            ip: 2001:100:2:31::1
            admin: up
            address_family:
              - type: ipv4
                activate: false
                state: present
              - type: ipv6
                activate: true
                state: present 
        state: present
	  
**Step 5**

Create a playbook called ``datacenter.yaml``.

:: 

	---
	- hosts: datacenter
	  gather_facts: no
	  connection: network_cli
	  roles:		
		- Dell-Networking.dellos-interface
		- Dell-Networking.dellos-bgp
		- Dell-Networking.dellos-snmp
                - Dell-Networking.dellos-system

**Step 6**

Run the playbook.

``ansible-playbook -i inventory.yaml datacenter.yaml``

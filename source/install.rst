############
Installation
############

You can install Ansible roles on the control machine using Dell EMC devices.

Ansible modules
***************

Dell EMC Ansible modules for dellos6, dellos9, and dellos10 are part of the Ansible core. Install Ansible 2.3 or later to use these modules. To use OpenSwitch Ansible "opx_cps" module, install Ansible 2.7 or later. See `Ansible documentation <http://docs.ansible.com/ansible/intro_installation.html>`_ for more information.

Ansible roles
*************

Install all Dell EMC Ansible roles.

::

  ansible-galaxy install -r dellemc_roles.txt

where ``dellemc_roles.txt`` is defined as:

:: 

  Dell-Networking.dellos-aaa
  Dell-Networking.dellos-acl
  Dell-Networking.dellos-bgp
  Dell-Networking.dellos-copy-config
  Dell-Networking.dellos-dcb
  Dell-Networking.dellos-dns
  Dell-Networking.dellos-ecmp
  Dell-Networking.dellos-flow-monitor
  Dell-Networking.dellos-image-upgrade
  Dell-Networking.dellos-interface
  Dell-Networking.dellos-lag
  Dell-Networking.dellos-lldp
  Dell-Networking.dellos-logging
  Dell-Networking.dellos-ntp
  Dell-Networking.dellos-prefix-list
  Dell-Networking.dellos-qos
  Dell-Networking.dellos-route-map
  Dell-Networking.dellos-sflow
  Dell-Networking.dellos-snmp
  Dell-Networking.dellos-system
  Dell-Networking.dellos-users
  Dell-Networking.dellos-vlan
  Dell-Networking.dellos-vlt
  Dell-Networking.dellos-vrf
  Dell-Networking.dellos-vrrp
  Dell-Networking.dellos-xstp

You can also install an individual Dell EMC Networking Ansible role using a single command. For example, to install the AAA role use ``ansible-galaxy install Dell-Networking.dellos.aaa``.

See `Ansible Galaxy <https://galaxy.ansible.com/Dell-Networking/>`_ for more information on Dell EMC Ansible roles.

Dell EMC devices
***************************

Dell EMC devices require minimal configuration to run Ansible playbooks.

OS6
---

#. Create a username and password for Ansible.

#. Configure the Management interface (static/dynamic IP address).

#. Enable the SSH server.

::

  console(config)# username admin password ansible@123
  console(config)# enable password ansible@123
  console(config)# interface  out-of-band
  console(conf-if)# ip address 10.16.148.79 255.255.255.0 10.16.148.254 
  console(conf-if)# exit
  console(config)# ip ssh  server 

OS9
---

1. Create a username and password for Ansible.

#. Configure the Management interface (static/dynamic IP address).

#. Enable the SSH server.

#. Set the maximum connection rate limit.

::

  Dell(config)# username ansible password ansible
  Dell(config)# enable password ansible
  Dell(config)# interface managementethernet 0/0
  Dell(conf-if-ma-0/0)# ip add 10.16.148.72/24
  Dell(conf-if-ma-0/0)# no shutdown 
  Dell(conf-if-ma-0/0)# exit
  Dell(config)# ip ssh server enable 
  Dell(config)# ip ssh connection-rate-limit 60

OS10
----

1. Create an Ansible username and password.

#. Configure the Management interface (static/dynamic IP address).

::

  OS10# config t
  OS10(config)# username ansible password ansible
  OS10(config)# interface mgmt 1/1/1
  OS10(conf-if-ma-1/1/1)# ip address 10.16.149.62/16
  OS10(conf-if-ma-1/1/1)# no shutdown
  OS10(conf-if-ma-1/1/1)# do commit
  OS10(conf-if-ma-1/1/1)# exit

> **NOTE**: SSH is enabled in OS10 by default.

OPX
----

1. Create an Ansible username and password.

#. Configure the Management interface (static/dynamic IP address).

::

  root@os10:/config/home/linuxadmin# useradd testuser
  root@os10:/config/home/linuxadmin# passwd testuser
  New password:
  Retype new password:
  passwd: password updated successfully
  root@os10:/config/home/linuxadmin# ifconfig eth0 10.16.148.123 netmask 255.255.255.0 up
  root@os10:/config/home/linuxadmin# route default gw 10.16.148.254 

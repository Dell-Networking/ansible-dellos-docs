======================================================================
Use Ansible to perform ZTD on devices running Dell EMC Networking OS10
======================================================================

This example describes how to use Ansible to perform Zero touch deployment.It installs or upgrades a software image on a
device running Dell EMC Networking OS10. The example playbook uses the *dellos-image-upgrade* role to upgrade or install an
OS10 image on a specified switch, followed by a *dellos-copy-config* role to push configs post installation on the device.
Before using Ansible to install the software image, you must download the software image via FTP/TFTP/SCP/HTTPDS, then spe
cify the path to the image in the playbook.

Installation
------------

**1**. Set up AWX

- Download AWX 4.0.0 release, make sure you have latest ansible version and Install AWX

  ::

    ansible-galaxy install -r dellemc_roles.txt
    apt-add-repository --yes --update ppa:ansible/ansible
    apt install ansible -y
    apt install docker.io
    apt install python-pip -y
    pip install docker
    pip install docker-compose
    wget https://github.com/ansible/awx/archive/4.0.0.zip # Download the zip file
    unzip 4.0.0.zip # unzip the downloaded file

  Open installer/inventory file and change docker parameters

  ::
   
    postgres_data_dir=/var/lib/pgdocker # change from /tmp to /var/lib
    docker_compose_dir=/var/lib/awxcompose # change from /tmp to /var/lib

  Under installer folder, run the following commad.

  ::
  
    cd installer
    ansible-playbook -i inventory install.yml -vvv

- Launch AWX in browser
- Go to Projects and Create AWX project e.g: Name, descriptionand scm type
- Create playbook in project directory
- Go to Inventories and Create inventory and Hostkey
- Go to template and Create job template

**2**. Add curl script to contact an Ansible server

- Go to ztd-provision-url(http://X.X.X.X/ztd.sh) defined in the DHCP server config and include the curl command to the ztd script.

  ::
  
    e.g: /usr/bin/curl -H "Content-Type:application/json" -k -X POST --data '{"host_config_key":"'7d07e79ebdc8f7c292e495daac0fe16b'"}' -u username:password https://X.X.X.X/api/v2/job_templates/xxx/callback/

**3**. Run ZTD from device

- Run the ZTD by rebooting the switch. Enter the reload ztd command.

  ::
  
    OS10#reload ztd

Example playbook
----------------

The *dellos-image-upgrade* role uses the ``dellos10_command`` to install or upgrade the switch, and ``wait_for`` is used to
identify the progress of the upgrade operation. The *dellos-copy-config* role uses the ``dellos10_config`` module to push
configs to the device.

  **Sample hosts file**

  ::
  
    ztdswitch ansible_host= <ip_address>

  **Sample host_vars for Dell-Networking.dellos-image-upgrade**

  ::
    
    hostname: ztdswitch
    ansible_become: yes
    ansible_become_method: xxxxx
    ansible_become_pass: xxxxx
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10
    dellos_image_upgrade:
      operation_type: install
      software_image_url: tftp://X.X.X.X/PKGS_OS10-Enterprise-10.2.9999E.5790-installer-x86_64.bin
      software_version: 10.2.9999E

  **Simple playbook to setup ZTD**

  ::
  
    - hosts: ztdswitch
      connection: network_cli
      roles:
         - Dell-Networking.dellos-image-upgrade
         - Dell-Networking.dellos-copy-config



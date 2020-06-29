Source: os10_facts.py
++++++++++++++++++++

.. _os10_facts_module:


os10_facts -- Collect facts from remote devices running Dell EMC Networking OS10
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


.. contents::
   :local:
   :depth: 1


Synopsis
--------
- Collects a base set of device facts from a remote device that is running OS10.  This module prepends all of the base network fact keys with ``ansible_net_<fact>``.  The facts module will always collect a base set of facts from the device and can enable or disable collection of additional facts.




Parameters
----------

.. raw:: html

    <table  border=1 cellpadding=0 class="documentation-table">
        <tr bgcolor="LightSkyBlue">
            <th colspan="2">Parameter</th>
            <th>Choices/<font color="blue">Defaults</font></th>
            <th width="100%">Comments</th>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-gather_subset"></div>
                <b>gather_subset</b>
                <a class="ansibleOptionLink" href="#parameter-gather_subset" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>
                <b>Default:</b><br/><div style="color: blue">["!config"]</div>
            </td>
            <td>
                <div>When supplied, this argument will restrict the facts collected to a given subset.  Possible values for this argument include all, hardware, config, and interfaces.  Can specify a list of values to include a larger subset.  Values can also be used with an initial <code><span class='module'>!</span></code> to specify that a specific subset should not be collected.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-provider"></div>
                <b>provider</b>
                <a class="ansibleOptionLink" href="#parameter-provider" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">dictionary</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>A dict object containing connection details.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-provider/auth_pass"></div>
                <b>auth_pass</b>
                <a class="ansibleOptionLink" href="#parameter-provider/auth_pass" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>Specifies the password to use if required to enter privileged mode on the remote device.  If <em>authorize</em> is false, then this argument does nothing. If the value is not specified in the task, the value of environment variable <code>ANSIBLE_NET_AUTH_PASS</code> will be used instead.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-provider/authorize"></div>
                <b>authorize</b>
                <a class="ansibleOptionLink" href="#parameter-provider/authorize" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">boolean</span>
                </div>
            </td>
            <td>
                <ul style="margin: 0; padding: 0"><b>Choices:</b>
                    <li><div style="color: blue"><b>no</b>&nbsp;&larr;</div></li>
                    <li>yes</li>
                </ul>
            </td>
            <td>
                <div>Instructs the module to enter privileged mode on the remote device before sending any commands.  If not specified, the device will attempt to execute all commands in non-privileged mode. If the value is not specified in the task, the value of environment variable <code>ANSIBLE_NET_AUTHORIZE</code> will be used instead.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-provider/host"></div>
                <b>host</b>
                <a class="ansibleOptionLink" href="#parameter-provider/host" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                       / <span style="color: red">required</span>                    </div>
            </td>
            <td>
            </td>
            <td>
                <div>Specifies the DNS host name or address for connecting to the remote device over the specified transport.  The value of host is used as the destination address for the transport.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-provider/password"></div>
                <b>password</b>
                <a class="ansibleOptionLink" href="#parameter-provider/password" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>Password to authenticate the SSH session to the remote device. If the value is not specified in the task, the value of environment variable <code>ANSIBLE_NET_PASSWORD</code> will be used instead.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-provider/port"></div>
                <b>port</b>
                <a class="ansibleOptionLink" href="#parameter-provider/port" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">integer</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>Specifies the port to use when building the connection to the remote device.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-provider/ssh_keyfile"></div>
                <b>ssh_keyfile</b>
                <a class="ansibleOptionLink" href="#parameter-provider/ssh_keyfile" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">path</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>Path to an ssh key used to authenticate the SSH session to the remote device.  If the value is not specified in the task, the value of environment variable <code>ANSIBLE_NET_SSH_KEYFILE</code> will be used instead.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-provider/timeout"></div>
                <b>timeout</b>
                <a class="ansibleOptionLink" href="#parameter-provider/timeout" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">integer</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>Specifies idle timeout (in seconds) for the connection. Useful if the console freezes before continuing. For example when saving configurations.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-provider/username"></div>
                <b>username</b>
                <a class="ansibleOptionLink" href="#parameter-provider/username" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>User to authenticate the SSH session to the remote device. If the value is not specified in the task, the value of environment variable <code>ANSIBLE_NET_USERNAME</code> will be used instead.</div>
            </td>
        </tr>

    </table>
    <br/>


Notes
-----

   - For more information on using Ansible to manage Dell EMC Network devices see https://www.ansible.com/ansible-dell-networking.



Examples
--------

.. code-block:: yaml+jinja

    
    # Collect all facts from the device
    - os10_facts:
        gather_subset: all

    # Collect only the config and default facts
    - os10_facts:
        gather_subset:
          - config

    # Do not collect hardware facts
    - os10_facts:
        gather_subset:
          - "!hardware"




Return Values
-------------
The following are the fields unique to this module:

.. raw:: html

    <table border=1 cellpadding=0 class="documentation-table">
        <tr bgcolor="LightSkyBlue">
            <th colspan="1">Key</th>
            <th width="20%">Returned</th>
            <th width="80%">Description</th>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_all_ipv4_addresses"></div>
                <b>ansible_net_all_ipv4_addresses</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_all_ipv4_addresses" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>When interfaces is configured</td>
            <td>
                <div>All IPv4 addresses configured on the device</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_all_ipv6_addresses"></div>
                <b>ansible_net_all_ipv6_addresses</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_all_ipv6_addresses" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>When interfaces is configured</td>
            <td>
                <div>All IPv6 addresses configured on the device</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_config"></div>
                <b>ansible_net_config</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_config" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>When config is configured</td>
            <td>
                <div>The current active config from the device</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_cpu_arch"></div>
                <b>ansible_net_cpu_arch</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_cpu_arch" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>When hardware is configured</td>
            <td>
                <div>CPU Architecture of the remote device.</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_gather_subset"></div>
                <b>ansible_net_gather_subset</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_gather_subset" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>Always</td>
            <td>
                <div>The list of fact subsets collected from the device</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_hostname"></div>
                <b>ansible_net_hostname</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_hostname" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>Always</td>
            <td>
                <div>The configured hostname of the device</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_interfaces"></div>
                <b>ansible_net_interfaces</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_interfaces" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">dictionary</span>
                </div>
            </td>
            <td>When interfaces is configured</td>
            <td>
                <div>A hash of all interfaces running on the system</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_memfree_mb"></div>
                <b>ansible_net_memfree_mb</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_memfree_mb" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">integer</span>
                </div>
            </td>
            <td>When hardware is configured</td>
            <td>
                <div>The available free memory on the remote device in Mb</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_memtotal_mb"></div>
                <b>ansible_net_memtotal_mb</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_memtotal_mb" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">integer</span>
                </div>
            </td>
            <td>When hardware is configured</td>
            <td>
                <div>The total memory on the remote device in Mb</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_model"></div>
                <b>ansible_net_model</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_model" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>Always</td>
            <td>
                <div>The model name returned from the device.</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_name"></div>
                <b>ansible_net_name</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_name" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>Always</td>
            <td>
                <div>The name of the OS that is running.</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_neighbors"></div>
                <b>ansible_net_neighbors</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_neighbors" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">dictionary</span>
                </div>
            </td>
            <td>When interfaces is configured</td>
            <td>
                <div>The list of LLDP neighbors from the remote device</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_servicetag"></div>
                <b>ansible_net_servicetag</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_servicetag" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>Always</td>
            <td>
                <div>The service tag number of the remote device.</div>
                <br/>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-ansible_net_version"></div>
                <b>ansible_net_version</b>
                <a class="ansibleOptionLink" href="#return-ansible_net_version" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>Always</td>
            <td>
                <div>The operating system version running on the remote device</div>
                <br/>
            </td>
        </tr>
    </table>
    <br/><br/>



Authors
~~~~~~~

- Senthil Kumar Ganesan (@skg-net)

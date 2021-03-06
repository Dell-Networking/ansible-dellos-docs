Source: os10_config.py
++++++++++++++++++++++

.. _os10_config_module:


os10_config -- Manage Dell EMC Networking OS10 configuration sections
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


.. contents::
   :local:
   :depth: 1


Synopsis
--------
- OS10 configurations use a simple block indent file syntax for segmenting configuration into sections.  This module provides an implementation for working with OS10 configuration sections in a deterministic way.




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
                <div class="ansibleOptionAnchor" id="parameter-after"></div>
                <b>after</b>
                <a class="ansibleOptionLink" href="#parameter-after" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>The ordered set of commands to append to the end of the command stack if a change needs to be made.  Just like with <em>before</em> this allows the playbook designer to append a set of commands to be executed after the command set.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-backup"></div>
                <b>backup</b>
                <a class="ansibleOptionLink" href="#parameter-backup" title="Permalink to this option"></a>
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
                <div>This argument will cause the module to create a full backup of the current <code>running-config</code> from the remote device before any changes are made. If the <code>backup_options</code> value is not given, the backup file is written to the <code>backup</code> folder in the playbook root directory. If the directory does not exist, it is created.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-backup_options"></div>
                <b>backup_options</b>
                <a class="ansibleOptionLink" href="#parameter-backup_options" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">dictionary</span>
                </div>
                <div style="font-style: italic; font-size: small; color: darkgreen">added in 2.8</div></td>
            <td>
            </td>
            <td>
                <div>This is a dict object containing configurable options related to backup file path. The value of this option is read only when <code>backup</code> is set to <em>yes</em>, if <code>backup</code> is set to <em>no</em> this option will be silently ignored.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-backup_options/dir_path"></div>
                <b>dir_path</b>
                <a class="ansibleOptionLink" href="#parameter-backup_options/dir_path" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">path</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>This option provides the path ending with directory name in which the backup configuration file will be stored. If the directory does not exist it will be first created and the filename is either the value of <code>filename</code> or default filename as described in <code>filename</code> options description. If the path value is not given in that case a <em>backup</em> directory will be created in the current working directory and backup configuration will be copied in <code>filename</code> within <em>backup</em> directory.</div>
            </td>
        </tr>
        <tr>
            <td class="elbow-placeholder"></td>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="parameter-backup_options/filename"></div>
                <b>filename</b>
                <a class="ansibleOptionLink" href="#parameter-backup_options/filename" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>The filename to be used to store the backup configuration. If the the filename is not given it will be generated based on the hostname, current time and date in format defined by &lt;hostname&gt;_config.&lt;current-date&gt;@&lt;current-time&gt;</div>
            </td>
        </tr>

        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-before"></div>
                <b>before</b>
                <a class="ansibleOptionLink" href="#parameter-before" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>The ordered set of commands to push on to the command stack if a change needs to be made.  This allows the playbook designer the opportunity to perform configuration commands prior to pushing any changes without affecting how the set of commands are matched against the system.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-config"></div>
                <b>config</b>
                <a class="ansibleOptionLink" href="#parameter-config" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>The module, by default, will connect to the remote device and retrieve the current running-config to use as a base for comparing against the contents of source.  There are times when it is not desirable to have the task get the current running-config for every task in a playbook.  The <em>config</em> argument allows the implementer to pass in the configuration to use as the base config for comparison.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-lines"></div>
                <b>lines</b>
                <a class="ansibleOptionLink" href="#parameter-lines" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>The ordered set of commands that should be configured in the section.  The commands must be the exact same commands as found in the device running-config. Be sure to note the configuration command syntax as some commands are automatically modified by the device config parser. This argument is mutually exclusive with <em>src</em>.</div>
                <div style="font-size: small; color: darkgreen"><br/>aliases: commands</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-match"></div>
                <b>match</b>
                <a class="ansibleOptionLink" href="#parameter-match" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>
                <ul style="margin: 0; padding: 0"><b>Choices:</b>
                    <li><div style="color: blue"><b>line</b>&nbsp;&larr;</div></li>
                    <li>strict</li>
                    <li>exact</li>
                    <li>none</li>
                </ul>
            </td>
            <td>
                <div>Instructs the module on the way to perform the matching of the set of commands against the current device config.  If match is set to <em>line</em>, commands are matched line by line.  If match is set to <em>strict</em>, command lines are matched with respect to position.  If match is set to <em>exact</em>, command lines must be an equal match.  Finally, if match is set to <em>none</em>, the module will not attempt to compare the source configuration with the running configuration on the remote device.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-parents"></div>
                <b>parents</b>
                <a class="ansibleOptionLink" href="#parameter-parents" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>The ordered set of parents that uniquely identify the section or hierarchy the commands should be checked against.  If the parents argument is omitted, the commands are checked against the set of top level or global commands.</div>
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
                       / <span style="color: red">required</span></div>
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

        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-replace"></div>
                <b>replace</b>
                <a class="ansibleOptionLink" href="#parameter-replace" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>
                <ul style="margin: 0; padding: 0"><b>Choices:</b>
                    <li><div style="color: blue"><b>line</b>&nbsp;&larr;</div></li>
                    <li>block</li>
                </ul>
            </td>
            <td>
                <div>Instructs the module on the way to perform the configuration on the device.  If the replace argument is set to <em>line</em> then the modified lines are pushed to the device in configuration mode.  If the replace argument is set to <em>block</em> then the entire command block is pushed to the device in configuration mode if any line is not correct.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-save"></div>
                <b>save</b>
                <a class="ansibleOptionLink" href="#parameter-save" title="Permalink to this option"></a>
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
                <div>The <code>save</code> argument instructs the module to save the running- config to the startup-config at the conclusion of the module running.  If check mode is specified, this argument is ignored.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-src"></div>
                <b>src</b>
                <a class="ansibleOptionLink" href="#parameter-src" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">path</span>
                </div>
            </td>
            <td>
            </td>
            <td>
                <div>Specifies the source path to the file that contains the configuration or configuration template to load.  The path to the source file can either be the full path on the Ansible control host or a relative path from the playbook or role root directory. This argument is mutually exclusive with <em>lines</em>.</div>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div class="ansibleOptionAnchor" id="parameter-update"></div>
                <b>update</b>
                <a class="ansibleOptionLink" href="#parameter-update" title="Permalink to this option"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>
                <ul style="margin: 0; padding: 0"><b>Choices:</b>
                    <li><div style="color: blue"><b>merge</b>&nbsp;&larr;</div></li>
                    <li>check</li>
                </ul>
            </td>
            <td>
                <div>The <em>update</em> argument controls how the configuration statements are processed on the remote device.  Valid choices for the <em>update</em> argument are <em>merge</em> and <em>check</em>.  When you set this argument to <em>merge</em>, the configuration changes merge with the current device running configuration.  When you set this argument to <em>check</em> the configuration updates are determined but not actually configured on the remote device.</div>
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

    
    - os10_config:
        lines: ['hostname {{ inventory_hostname }}']

    - os10_config:
        lines:
          - 10 permit ip host 1.1.1.1 any log
          - 20 permit ip host 2.2.2.2 any log
          - 30 permit ip host 3.3.3.3 any log
          - 40 permit ip host 4.4.4.4 any log
          - 50 permit ip host 5.5.5.5 any log
        parents: ['ip access-list test']
        before: ['no ip access-list test']
        match: exact

    - os10_config:
        lines:
          - 10 permit ip host 1.1.1.1 any log
          - 20 permit ip host 2.2.2.2 any log
          - 30 permit ip host 3.3.3.3 any log
          - 40 permit ip host 4.4.4.4 any log
        parents: ['ip access-list test']
        before: ['no ip access-list test']
        replace: block

    - os10_config:
        lines: ['hostname {{ inventory_hostname }}']
        backup: yes
        backup_options:
          filename: backup.cfg
          dir_path: /home/user




Return Values
-------------
Common return values are documented :ref:`here <common_return_values>`, the following are the fields unique to this module:

.. raw:: html

    <table border=1 cellpadding=0 class="documentation-table">
        <tr bgcolor="LightSkyBlue">
            <th colspan="1">Key</th>
            <th width="20%">Returned</th>
            <th width="80%">Description</th>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-backup_path"></div>
                <b>backup_path</b>
                <a class="ansibleOptionLink" href="#return-backup_path" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">string</span>
                </div>
            </td>
            <td>when backup is yes</td>
            <td>
                <div>The full path to the backup file</div>
                <br/>
                <div style="font-size: smaller"><b>Sample:</b></div>
                <div style="font-size: smaller; color: blue; word-wrap: break-word; word-break: break-all;">/playbooks/ansible/backup/os10_config.2016-07-16@22:28:34</div>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-commands"></div>
                <b>commands</b>
                <a class="ansibleOptionLink" href="#return-commands" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>Always</td>
            <td>
                <div>The set of commands that will be pushed to the remote device</div>
                <br/>
                <div style="font-size: smaller"><b>Sample:</b></div>
                <div style="font-size: smaller; color: blue; word-wrap: break-word; word-break: break-all;">[&#x27;hostname foo&#x27;, &#x27;router bgp 1&#x27;, &#x27;router-id 1.1.1.1&#x27;]</div>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-saved"></div>
                <b>saved</b>
                <a class="ansibleOptionLink" href="#return-saved" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">boolean</span>
                </div>
            </td>
            <td>When not check_mode.</td>
            <td>
                <div>Returns whether the configuration is saved to the startup configuration or not.</div>
                <br/>
                <div style="font-size: smaller"><b>Sample:</b></div>
                <div style="font-size: smaller; color: blue; word-wrap: break-word; word-break: break-all;">True</div>
            </td>
        </tr>
        <tr>
            <td colspan="1">
                <div class="ansibleOptionAnchor" id="return-updates"></div>
                <b>updates</b>
                <a class="ansibleOptionLink" href="#return-updates" title="Permalink to this return value"></a>
                <div style="font-size: small">
                    <span style="color: purple">list</span>
                </div>
            </td>
            <td>Always</td>
            <td>
                <div>The set of commands that will be pushed to the remote device.</div>
                <br/>
                <div style="font-size: smaller"><b>Sample:</b></div>
                <div style="font-size: smaller; color: blue; word-wrap: break-word; word-break: break-all;">[&#x27;hostname foo&#x27;, &#x27;router bgp 1&#x27;, &#x27;router-id 1.1.1.1&#x27;]</div>
            </td>
        </tr>
    </table>
    <br/><br/>


Authors
~~~~~~~

- Senthil Kumar Ganesan (@skg-net)

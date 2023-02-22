Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

Geen handlers folder gebruikt aangezien er geen triggers worden aangemaakt 


defaults/main.yml: A YAML file that contains default variables that can be overridden by the user. For example, you can set default VLANs or port configurations for the network devices.

files/: A folder that contains files that will be copied to the network devices during the role execution. For example, you can copy a Cisco IOS image to the device.

handlers/main.yml: A YAML file that contains handlers that can be triggered by tasks. Handlers are similar to tasks but are only executed when called by a notification from another task.

meta/main.yml: A YAML file that contains metadata about the role. This can include dependencies on other roles or collections, and can specify whether the role is platform-specific.

tasks/main.yml: A YAML file that contains the main tasks of the role. These are the steps that will be executed when the role is run. For example, you can configure VLANs, access control lists (ACLs), or interfaces on the network devices.

templates/: A folder that contains Jinja2 templates that will be rendered and copied to the network devices during the role execution. For example, you can create a template for a Cisco IOS configuration file.

tests/inventory: An inventory file that specifies the devices that will be targeted by the role.

tests/test.yml: A YAML file that contains a playbook that will be used to test the role. This can include tasks that verify the configuration of the network devices.

vars/main.yml: A YAML file that contains variables that are used in the tasks. These variables can be set based on the device type, device location, or any other relevant criteria. For example, you can set variables for a specific switch model or VLAN configurations.

Here is an example of how this directory layout could be used to configure VLANs on a network switch:

In defaults/main.yml, you could set the default VLAN configurations:

yaml
Copy code
---
vlan_config:
  - id: 10
    name: "Data"
  - id: 20
    name: "Voice"
In tasks/main.yml, you could create a task that applies the VLAN configurations:

yaml
Copy code
---
- name: Configure VLANs
  ios_vlan:
    vlan_id: "{{ item.id }}"
    vlan_name: "{{ item.name }}"
    state: present
  with_items: "{{ vlan_config }}"
In vars/main.yml, you could set variables for a specific switch model:

yaml
Copy code
---
switch_model: "cisco_nexus"
And in templates/config.j2, you could create a Jinja2 template that will be rendered and copied to the switch:

python
Copy code
{% if switch_model == "cisco_nexus" %}
vlan {{ item.id }}
 name {{ item.name }}
{% endif %}
Overall, this directory layout helps to organize the role into different folders based on their functionality, making it easier to read and maintain.






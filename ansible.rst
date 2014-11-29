=======================
Introduction to Ansible
=======================

System configuration doesn't have to complicated

:name: Praveen Kumar
:contact: kumarpraveen [AT] fedoraproject DOT org
:date: 2014-09-28


Agenda
======

- What is Ansible
- Installation
- Ansible Basic
- Inventory
- Ad-hoc Commands
- Ansible-Playbook
- Modules
- Variables
- Roles
- Demo


Ansible
=======

.. image:: images/Ansible.png
    :height: 300px
    :width: 400px
    :scale: 50%
    :align: center

IT automation tool.

- Application Deployment
- Multi-Tier Orchestration
- Configuration Management
- Except Python 2.4 or later

- http://en.wikipedia.org/wiki/Ansible_(software)

WHY Ansible?
============
- New servers, New application, Updates?
- Is it cloud Infra?
- Is it hybrid?
- No custom PKI-SSH-based
- Configuration as data, not code (simply written in playbook)
- Rescue from agent-base tool (like Puppet, Chef)
- Batteries Included

Install Ansible
===============

- yum install ansible
- apt-get install ansible
- pip install ansible

Sample Playbook
===============

.. code:: yaml

    ---
    - name: install and start httpd service
      hosts: webservers
      user: cloud-user
      sudo: yes
      vars:
        http_port: 80
        max_clients: 200
      tasks:
      - name: ensure apache is at the latest version
        yum: name=httpd state=present
      - name: write the apache config file
        service: name=httpd state=started
      - name: Enable throw firewalld
        firewalld: service=http permanent=true state=enabled


Ad-hoc Commands
===============

- ansible <server_name> -m ping -u <remote_user>
- ansible <server_name> -m copy -a "src=/etc/hosts dest=/tmp/hosts"

Inventory
=========

- Ansible works against multiple systems in your infrastructure at the same
  time.
- Default:- /etc/ansible/hosts
- http://docs.ansible.com/intro_inventory.html

Inventory Cont...
=================

- Non-standards ssh port
    webserver.example.com:2222

Variables
=========

- Playbook variables
- Inventory (group vars, host vars)
- Command line (Extra variable)
- Decovered Variables (facts)


Using Variables
===============

In a playbook

tasks:

.. code:: yaml

    - name: which machine
      command: echo "My IP is {{ansible_default_ip4.address }}"

In a template

This machine IP is  {{ ansible_default_ip4.address }}.

Roles
=====

- Project organizational tool
- Reusable components
- Defined filesystem structure

Docs
====

- http://docs.ansible.com/
- http://docs.ansible.com/list_of_all_modules.html

Sample Examples
===============

- https://github.com/ansible/ansible-examples
- http://infrastructure.fedoraproject.org/infra/ansible.git

Demo Time
=========

- ansible-playbook -i hosts foo.yml

Questions
=========
**?**

Thank You
=========

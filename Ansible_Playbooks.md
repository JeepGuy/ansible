# Ansible Playbooks
=================

Playbook - a set of instructions for ansible to execute on a or a group of
          of servers.

Playbook - A single YAML File (contains a play)
  - Play - Defines a set of activities (tasks) to be run on hosts
     - Task - an action to be performed on the hosts
         > Execute a commands
         > Run a script
         > Install a package
         > Shutdown/Restart

sample playbook:

```
# Simple Ansible Playbook1.yml
-
  name: Play 1
  hosts: localhost, or webhost etc (defined in inventory must be at Play level)
  tasks:
    - name: Execute command 'date'
      command: date

    - name: Execute script on server
      script: test_script.sh

    - name: Install httpd service
      yum:
        name: httpd
        state: present

    - name: Start web server
      service:
        name: httpd
        stated: started
  #############################
```
A Playbook is a list of dictionaries in YAML terms

Tasks are a list (ordered collection so order matters)

## Simple Ansible Playbook1.yml
```
-
  name: Play 1
  hosts: localhost, or webhost etc (defined in inventory must be at Play level)
  tasks:
    - name: Execute command 'date'
      command: date

    - name: Execute script on server
      script: test_script.sh

-
   name: Play 2
    - name: Install httpd service
      yum:
        name: httpd
        state: present

    - name: Start web server
      service:
        name: httpd
        stated: started
```

Ansible Modules:
Different actions run by tasks.

i.e. - command, script, yum, service...
There are hundreds of modules out of the box from Ansible.
 > on the website OR
 run command:  ansible-doc-l  (L) on your ansible system for a listed

 ### RUN the Ansible Playbook
 ------------------------

Execute Ansible Playbook:
Syntax: ansible-playbook <playbook_file_name>.yml

ansible-playbook --help   :::: for help...



#### Update the playbook with a play to "Execute a script on all web server nodes". The script is located at /tmp/install_script.sh
```
-
name: Execute a script on all web server nodes
hosts: web_nodes
tasks:
-
name: Execute a script on all web server nodes
script: /tmp/install_script.sh

---

-
  name: Execute a script on all web server nodes
  hosts: web_nodes
  tasks:
    -
      name: Execute a script on all web server nodes
      script: /tmp/install_script.sh

...

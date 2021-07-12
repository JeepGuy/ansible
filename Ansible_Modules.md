Ansible Modules
===============

Categorized into various groups based on their functionality

- System
   User, Group, Hostname, Iptables, Lvg, Lvol, Make, Mount, Ping, Timezone, Systemd, Service
   Lvg = Logical volume groups
- Commands
   Command, expect, raw, script, shell
- Files
  Acl, Archive, Copy, File, Find, Lineinfile, Replace, Stat, Template, Unarchive
   Archive = compress,  Unarchive = unpack
   File, Find, Lineinfile = modify the contents of an existing files
- Database- Add or modify databases or configurations
   - Mongodb, Mssql, Mysql, Postgresql, Proysql, vertica
- Cloud - manage everything in a cloud
   - Amazon, Docker, Openstack, VMware
- Windows
   - use in a Windows
   - Win_copy, Win_regedit, Win_user, etc...
- more..

##############

Command Module:
---------------
Executes a command on a remote node.
 NOTE: creates=/folder - checks to see if the folder exists before executing the mkdir command

copy: requires a source and destination
      src=/source_file dest=/destination

Script Module
-------------

Runs a local script on a remote node after transferring it.
- ansible takes care of the copy process for you...

1. Copy script to remote system
2. Exeute script on remote systems

SAMPLE Module
-------------

-
  name: Play1
  hosts: localhost
  tasks:
     - Name: Run a script on remote server
       script: /somelocalscriptsh -arg1 -arg2

Service Module
--------------

- Manages Services - Start, Stop, Restart

Can start services in order.

Must pass input in a key - value pair format.

.e.g. service: name=postgresql state=started

OR
      dictionary format:
   name: postgresql
   state: started
In yaml format name and state are properties of a dictionary.

EXAMPLE ******
-
  name: Execute a script on all web server nodes and start httpd service
  hosts: web_nodes
  tasks:
    -
      name: Execute a script
      script: /tmp/install_script.sh

    -
      name: Start httpd
      service:
         name: httpd
         state: started

-------

Why is the action STARTED and not start.
 - we are ensuring that the service is stated... we are not telling it to just try to
   start the service.
 - - this means if http service is not already started => start it
     if httpd is started => do nothing.

This is called: (Ansible documentation)
Idempotency
 - An operation is idempotent if the result of performing it once is exactly the
   same as the  result of performing it repeatedly without any intervening actions.

This is so you can run the same playbook and Ansible can report that the result of the
operation is in the correct state, if it is not Ansible takes care of putting it
into the expected state.

LINEINFILE Command
------------------

- Search for a line in a file and replace it or add it if it doesn't exist.

e.g. insert a new Nameserver into the resolve.conf file.

If you ran a script it would keep adding the line in the resolve.conf file.
If you run this in an Ansible Playbook it will ensure that there is only on line
in the file.

-
  name: Setup web server on all nodes
  hosts: web_nodes
  tasks:
    -
      name: Update entry into /etc/resolv.conf
      lineinfile:
        path: /etc/resolv.conf
        line: 'nameserver 10.1.250.10'

    -
      user:
        name: web_user
        uid: 1040
        group: developers
    -
      name: Execute a script
      script: /tmp/install_script.sh

    -
      name: Start httpd service             ###################################
      service:
        name: httpd
        state: present




.....

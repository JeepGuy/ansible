Ansible Conditionals
====================
#####################################################################
# Sample Inventory File
web1 ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
db1 ansible_host=db.company.com ansible_connection=winrm ansible_user=administrator ansible_password=Password123!
web2 ansible_host=server2.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!

[all_servers] # Group
web1
db
web2
#########################################
# sample Ansible Playbook1

-
  name: Start Services
  hosts: all_servers
  tasks:
     -   service: name=mysql state=started

     -   service: name=httpd state=Started
#####################################################################

If ansible tries to run this playbook it will fail because the servers are different
and have different services.

So add condition to each task which tells Ansible what to do...

REMEMBER: use double equals operator for comparison.

# sample Ansible Playbook1_MODIFIED

-
  name: Start Services
  hosts: all_servers
  tasks:
     -   service: name=mysql state=started
         when: ansible_host == "db.company.com"

     -   service: name=httpd state=Started
         when: ansible_connection == "web1.company.com" or  (can use an and here)
               ansible_conneciton == "web2.company.com"

#####################################################################

THE CORRECT WAY TO DO THIS WOULD BE TO GROUP THE SERVERS IN EB SERVERS ADN DB SERVERS....
AND RUN SEPERATE PLAYS FOR EACH GROUPS OF SERVERS.
 - THIS IS JUST AN EXAMPLE.

REGISTER CAN BE USED TO STORE THE OUTPUT OF A MODULE.
register: <variable>


# sample Ansible Playbook2

-
  name: Check status of service and email if down
  hosts: localhost
  tasks:
     -   command: service httpd status
         register: command_output

     -   mail:
              to: Admins <system.admins@company.com>
              subject: Service Alert
              body: 'Service {{ ansible_hostname }} is down'
         when: command_output.stdout.find('down') != -1

#####################################################################
#####################################################################
#####################################################################

EXERCISE EXAMPLES
==================

# We have created a group for web servers. Similarly create a group for database servers named 'db_servers' and add db1 server to it
# --------------------------------
# Sample Inventory File

# Web Servers
web1 ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
web2 ansible_host=server2.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
web3 ansible_host=server3.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!

# Database Servers
db1 ansible_host=server4.company.com ansible_connection=winrm ansible_user=administrator ansible_ssh_pass=Password123!

[web_servers]
web1
web2
web3

[db_servers]
db1

#####################################################################

another EXAMPLE

when: ansible_connection == "web1.company.com" or  (can use an and here)
      ansible_conneciton == "web2.company.com"

when: age is < 18 or >= 18

-
  name: Am in an Adult or a Child
  hosts: localhost
  vars:
    age: 25
  tasks:
    -
      command: echo "I am a Child"
      when: age < 18
    -
      command: echo "I am an Adult"
      when: age >= 18

  ##########


  -
  name: Add name server entry if not already entered
  hosts: localhost
  tasks:
    - shell: cat /etc/resolv.conf
      register: command_output

    -
      shell: echo "nameserver 10.0.250.10" >> /etc/resolv.conf
      when:  command_output.stdout.find('10.0.250.10') == -1    (must have single quote around the ip value
      )







...

Ansible Inventory
=================

Ansible can work with one or multiple systems in your infrastructure at the same time.
- is agentless because it uses ssh to connect to those servers.

Information about the target systems is stored in an inventory file.
 > If you don't create an invenotry file ansible will use the default file found at:
     /etc/ansible/hosts

The inventory file is in the ini format.
 - It is simply a list of servers listed one after the other.

 # Sample file

Server1.company.com
Server2.company.com

[mail]                 (Defining a group in the inventory file)
Server3.company.com
Server4.company.com

Then you can target different groups of servers at once using the groups
you define in the inventory file.


Using an alias in the inventory file.
for is name and defined type and the FQDN

web ansible_host=Server1.company.com

You can further differentiate the type of server based on the connection type.
------------------------------------

web ansible_host=Server1.company.com  ansible_connection=ssh

The Inventory Parameters you can use are:
-----------------------------------------
(inside the file)

ansible_connection - ssh/winrm/
localhost
ansible_port - 22/5986
ansible_user - root/administrator
ansible_ssh_pass - Password

Store passwords in Ansible Vault (encrypt the password use a password to decrypt at runtime.)


SAMPLE
# Web Servers
web1 ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
web2 ansible_host=server2.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
web3 ansible_host=server3.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!

# Database Servers
db1 ansible_host=server4.company.com ansible_connection=winrm ansible_user=administrator ansible_password=Password123!

SAMPLE2


# Web Servers
web1 ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
web2 ansible_host=server2.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
web3 ansible_host=server3.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!

# Database Servers
db1 ansible_host=server4.company.com ansible_connection=winrm ansible_user=administrator ansible_password=Password123!


[web_servers]
web1
web2
web3

[db_servers]
db1

[all_servers:children]
web_servers
db_servers

##########

# Web Servers

web_node1 ansible_host=web01.xyz.com ansible_connection=winrm ansible_user=administrator ansible_password=Win$Pass
web_node2 ansible_host=web02.xyz.com ansible_connection=winrm ansible_user=administrator ansible_password=Win$Pass
web_node3 ansible_host=web03.xyz.com ansible_connection=winrm ansible_user=administrator ansible_password=Win$Pass

# DB Servers
sql_db1 ansible_host=sql01.xyz.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Lin$Pass
sql_db2 ansible_host=sql02.xyz.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Lin$Pass

# Groups
[db_nodes]
sql_db1
sql_db2

[web_nodes]
web_node1
web_node2
web_node3

[boston_nodes]
 sql_db1
 web_node1

[dallas_nodes]
 sql_db2
 web_node2
 web_node3

[us_nodes:children]
boston_nodes
dallas_nodes

---

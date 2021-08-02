# Running playbooks on your local machine.

Localhost
When you don’t have access to a managed machine, you can use your Ansible host to run playbooks against itself. 


## The process  
 -  create an inventory file or use an existing one 
 -  add your local machine ( localhost )

Inventory File
Add a host group called mylocalhost. 
 *   localhost listed as a managed host, and  tell Ansible is a local connection.

[mylocalhost]
localhost ansible_connection=local

Once the inventory file and configuration are in place 
   -  run any playbook or a single command using the following command.

ansible mylocalhost -m ping -i servers

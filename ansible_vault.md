# Ansible Vault

Storing Credentials...
 - In plaintext format is insecure adn a bad practice.

```
# Inventory File - inventory.txt

db_server ansible_ssh_pass=Passw0rd  ansible+host=192.168.1.1
```


### Can store this data in an encrypted format. 
------------------------------------------------

Cmd:
ansible-vault encrypt inventory.txt

- when this command is run you will be asked for a new vault password

When you enter a new password the contents of the file are encrypted and the contents
are a series of numbers....

You can no longer run the playbook that call this inventory file using the normal syntax:

```ansible-playbook playbook-name.yml -i inventory.txt```

STDOUT:
ERROR! Attempted to read as ini file: Decryption failed... 


### To run and encrypted inventory file you must append the "-ask-vault-pass" to the command:

```ansible-playbook playbook-name.yml -i inventory.txt  -ask-vault-pass```

You will be prompted:
Vault password:      (enter the password Here)


### Can store the password in a file... can run it with the password vault file option:

```ansible-playbook playbook-name.yml -i inventory.txt  -ask-vault-file ~./vault_pass.txt```



https://www.udemy.com/course/learn-ansible-advanced/learn/lecture/7741998#overview  Finish lesson 24 or section 24 .







Ansible variables
=================

- Stores information that varies with each host
- Inventory   - used for ansible_host etc....

To all variables to a playbook you can add a yaml line called
vars:
 - with a key : value format to define the variable.

EXAMPLE
--------
#sample Ansible Playbook1.yaml
-
  names: Add DNS server to resolv.conf
  hosts: localhost
  vars:
     dns_server: 10.1.250.10
  tasks:
         -lineinfile:
              path: /etc/resolv.conf
              line: 'nameserver 10.1.250.10'
##############################################

Can add variables to a separate file ... for includes and roles.

# Sample  Variable_file.yaml
variable1: value1
variable2: value2

##################################

Define in playbook.
Use
EXAMPLE
--------
#sample Ansible Playbook1.yaml
-
  names: Add DNS server to resolv.conf
  hosts: localhost
  vars:
     dns_server: 10.1.250.10
  tasks:
         -lineinfile:
              path: /etc/resolv.conf
              line: 'nameserver {{dns_server}}'
                          # subsitute 'nameserver 10.1.250.10' with var as shown
####################################

The format for the variable replacement is called: Jinja2 Templating (look up)

To use a replacement for a value alone you must put it in single quotes
- If it is used in a sentence then the single quote is not required.

source: {{interger}}  WRONG
source: '{{interger}}'' CORRECT

source: something.{{interger}}.something CORRECT

#   #################################### exercise example

# Sample Inventory File

localhost ansible_connection=localhost nameserver_ip=10.1.250.10


#   #################################### exercise example
-
  name: Update nameserver entry into resolv.conf file on localhost
  hosts: localhost
  vars:
     car_model: BMW M3
     country_name: USA
     title: Systems Engineer
  tasks:
    -
      name: Print my car model
      command: echo "My car's model is {{car_model}}"

    -
      name: Print my country
      command: echo "I live in the {{country_name}}"

    -
      name: Print my title
      command: echo "I work as a {{title}}"



...

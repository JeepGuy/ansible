Ansible Roles
=============

Can write scripts in a single file.
However, the preferred method is to implement a script of program by breaking
it into:
   Packages
   Modules
   Classes
   Functions
This way our code becomes modularized, re-usable, and easy to read.

Even though there is no code in Ansible per se thi sis implemented in Ansible
with the help of roles.
 Ansible has:
   - Inventory Files
   - Variables
   - Playbooks
If we have lots to implement our Ansible is going to get more difficult to
manage.
 Writing a single large playbook may not be ideal in that case.
   THIS is where Include statements and Roles come into play.

INCLUDE
-------
To use: cut a large playbook into smaller files that address different use cases.
THEN has a master playbook that includes these smaller playbooks.

syntax:
   - include <playbook_name>

CAN INCLUDE TASKS AND VARIABLES
-----

ROLES
=====

define a structure for your project
define standards about how files and folders are organized within the project.

galaxy.ansible.com   Has sample roles etc...

### Create a role

ansible-galaxy init <Name-of-Role>








....

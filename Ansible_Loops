Ansible Loops
==============

WITH_ITEMS = a looping directive which executes the same tasks multiple number of times
   each time it iterates it stores the value in the items variable with the
   double braces  {{ item }}.


   - name: add several users
     user:
       name: "{{ item }}"
       state: present
       groups: "wheel"
     with_items:
        - testuser1
        - testuser2

#################################
 -
   hosts: localhost
   fruits:
     - Apple
     - Banana
     - Grapes
     - Orange
   tasks:
     -
       command: echo "Apple"

##################################

-
  hosts: localhost
  fruits:
    - Apple
    - Banana
    - Grapes
    - Orange
  tasks:
    -
      command: echo '{{ item }}'
      with_items: '{{ fruits }}'


-
  name: Print list of fruits
  hosts: localhost
  fruits:
    - Apple
    - Banana
    - Grapes
    - Orange
  tasks:
    -
      command: echo "{{ item }}"
      with_items: '{{ fruits }}'

########################

-
  name: Install required packages
  hosts: localhost
  vars:
      packages:
      - httpd
      - binutils
      - glibc
      - ksh
      - libaio
      - libXext
      - gcc
      - make
      - sysstat
      - unixODBC
      - mongodb
      - nodejs
      - grunt

  tasks:
    -
      yum:
        name: "{{ item }}"
        state: present
      with_items: "{{ packages }}"


#####

-
  name: Install required packages
  hosts: localhost
  vars:
      packages:
      - httpd
      - binutils
      - glibc
      - ksh
      - libaio
      - libXext
      - gcc
      - make
      - sysstat
      - unixODBC
      - mongodb
      - nodejs
      - grunt

  tasks:
    -
      yum: name=httpd state=present






.....

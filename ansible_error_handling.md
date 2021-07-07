# Ansible Error Handling


Related to Strategy... 

The flow of tasks...    What happens when tasks fail... 

Single Server:
* ----------------
Ansible executes all tasks.
If a task fails then the playbook  stops and exits.



Multiple Servers:
* ----------------

When a series of tasks are execute again mutiple servers
and if one of the tasks fails on one particular server, 
then 
  ansible takes that server out of the list 
  and continues to execute the tasks 
  on the remaining healty and available servers. 

- Ansible will attempt to complete as many servers as possile.


# Change the default behavior
# -------------------------------------------------

### To fail the playbook of ANY server fails

 - add an option called errors_fatal


# Sample Ansible Playbook with the errors_fatal option.
-
  name: Deploy Web Applications
  hosts: server1, server2, server3
  any_error_fatal: true     ################## the errors_fatal option.
  tasks:
    -  Install dependencies
	 ... <code hidden> ...
 
    -  Install Mysql databse
	 ... <code hidden> ...

    -  start Mysql database
	 ... <code hidden> ... 

### To CONTINUE the playbook if any TASK fails

set ignore_errors directive to yes on the task.

# Sample Ansible Playbook with ignore errors on a particular task option.
-
  name: Deploy Web Applications
  hosts: server1, server2, server3
  tasks:
    -  Install dependencies
	 ... <code hidden> ...
 
    -  Install Mysql databse
	 ... <code hidden> ...

    -  start Mysql database
	 ... <code hidden>
        ignore_errors: yes      ######################## ignore errors on a task directive.


### To FAIL the playbook if any TASK fails and exit the playbook

Set the failed_when directive along with a register-result variable.

# Sample Ansible Playbook with fail on a particular task using the failed_when directive.
-
  name: Deploy Web Applications
  hosts: server1, server2, server3
  tasks:
    -  Install dependencies
	 ... <code hidden> ...
        register: command_output    ############################# the register-result variable
        failed_when: "'ERROR' in command_output.stdout   ########  The failed_when directive = failure is true.
 
    -  Install Mysql databse
	 ... <code hidden> ...

    -  start Mysql database
	 ... <code hidden>
        ignore_errors: yes      ######################## ignore errors on a task directive.


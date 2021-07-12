Ansible Strategy 

Strategy: Linear
------------------
***** the Default Strategy is Linear. 
 - runs each task across all servers at the same time. 
   Said differently: Executes tasks across all servers on all hosts (in a pool of machines) in parallel  
   and waits for each task to complete on all servers before starting on the next task.


# Sample Ansible Playbook  (WITHOUT STRATEGY DIRECTIVE) therefore this is by default linear.
-
  name: Deploy Web Applications
  hosts: server1, server2, server3
  tasks:
    -  Install dependencies
	 ... <code hidden> ...
 
    -  Install Mysql databse
	 ... <code hidden> ...

    -  start Mysql database
	 ... <code hidden> ...    



Strategy:  "free"
------------------
  * In order to use a different strategy use the strategy directive and specify the name... 
    ... in this case "free"
The "free" strategy runs all the tasks independently on each server and does not wait for the tasks to finish on 
the other servers... 


# Ansible Playbook  # with strategy directive
-
  name: Deploy Web Applications
  strategy: free                        ############ Strategy Directive
  hosts: server1, server2, server3
  tasks:
    -  Install dependencies
	 ... <code hidden> ...
 
    -  Install Mysql databse
	 ... <code hidden> ...

    -  start Mysql database
	 ... <code hidden> ... 


Strategy: "batch"
------------------
This is  not a seperate strategy is a based on the default linear strategy 
however you can control the number of servers executed at once , or in a batch.
 
############ serial / batch number of servers you would like to process together.
   serial: 3  - here three servers would be processed together
- Ansible would run all the tasks on 3 servers and once that is complete it would run on the next batch

# Ansible Playbook  # with strategy directive
-
  name: Deploy Web Applications
  serial: 3                        ############ serial / batch number of servers you would like to process together .
  hosts: server1, server2, server3
  tasks:
    -  Install dependencies
	 ... <code hidden> ...
 
    -  Install Mysql databse
	 ... <code hidden> ...

    -  start Mysql database
	 ... <code hidden> ... 

Other Options"
 - can use a percentage

   serial: 25%  - this would run on 25% of the servers in the list of hosts... 

Custom Strategy
---------------

*** You can develop your own custom strategy by developing you own custom strategy yourself.


 
Maximum Number of Servers that can be run concurrently... 5 by default
*********************************************************

If you ahve 100 Servers in a hosts file, ansible by default will run five (5) servers at once, then 
move on the the next three servers etc.. 
UNLESS you specifiy a different number explicitly.

Ansible uses parrell process, or forks , to communicate with remote hosts.

You can increase this number in the Ansible.cfg file to as much cpu and ram you have abailable.

ansible.cfg
forks = 5
















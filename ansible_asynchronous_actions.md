Ansible Asynchronous actions 

Asynch and Poll 

# Ansible Playbook
-
  name: Deploy Web Application
  hosts: db_and_web_server
  tasks:
    -  command: /opt/monitor_webbapp/py
       async: 360
       poll: 60       ( Can set to zero see below explaination. )
       register: webbapp_result      # results variable



     - command: /opt/monitor_database.py
       async: 360
       poll: 60 
       register: database_result

# Then add a task to check the variabale status.

     - name: Check status of the tasks
       async_status: jid={{ webapp_result.asible_job_id }}    # this is the asynch_status module
       register: Job_result
       until: job_result.finished
       retries: 30 

# NOT ALL MODULES SUPPORT ASYNC   !!!


# ================================

async = How long to trun
poll = how freqeuntly to check
       DEFAULT 10 Seconds.

Run concurrent Tasks:   

You can set the poll value to zero and ansible will not wait for the first task to complete before is runs the second task.
   - However Ansible will exit immediately after kicking off the second task.

In order to wait for the tasks to be completed correctly... you must register the results of the task to a variable.  


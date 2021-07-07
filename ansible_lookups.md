# Ansible Lookups

## The lookup Plugin

#### Example: Storing credentials outside the inventory file

Store in a .csv file:
   There is a specific format:


```
# CSV File - credentials.csv file.
Hostname,Password
Target1, Passw0rd
Target2, Passw0rd
```

This is how to use the the lookup plugin.

{{ lookup('csvfile','target1 file=/tmp/credentials.csv delimiter=,') }}

           ^ this is the type of file. Other options available... see docs... 


{{ lookup('csvfile','target1 file=/tmp/credentials.csv delimiter=,') }}

                      ^ the value to lookup.

In this case above... The function will return the password from the .csv file.

A few other lookup plugins
--------------------------

 - INI
 - DNS
 - MongoDB

More Information about thsi is the Ansbile docuemntation under the Playbooks: Special Topics - Lookups.

# ansible
Ansible Notes and Examples

# Theory ~ Notes

## Code Elements
- Inventory Files
- Variables
- Playbooks

### Break down large Playbooks into manaable chunks
1. Include statements
2  Roles

### Include Files
Basically smaller playbooks
- Cut the playbook into smaller pieces that have differnt use cases
  i.e.provision-vms.yml
      install-dependencies.yml
      configure-web-server.yml
      setup-and-start-apps.yml
      
## Master Playbook
- includes smaller playbooks
- can also include tasks and variable lists.

i.e. setup-apps-and-start-apps.yml  (Yaml list)
     - include provision-vms.yml
     - include ... 
     

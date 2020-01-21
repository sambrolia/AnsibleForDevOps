Use vagrant setup from 2-AnsibleCommands

```
# Run Playbook
ansible-playbook playbook.yml --limit app

# Run Playbook, limit 
ansible-playbook playbook.yml --limit app

# Run Playbook show which hosts will be effected 
ansible-playbook playbook.yml --list-hosts
```
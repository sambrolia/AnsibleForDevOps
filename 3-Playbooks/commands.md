Use vagrant setup from 2-AnsibleCommands

```
# Run Playbook
ansible-playbook playbook.yml --limit app

# Run Playbook, limit 
ansible-playbook playbook.yml --limit app

# Run Playbook show which hosts will be effected 
ansible-playbook playbook.yml --list-hosts

# Run Playbook as specific users
ansible-playbook playbook.yml --user=johndoe

# Run Playbook ask for sudo password
ansible-playbook playbook.yml --ask-become-pass

# Run Playbook run every task as sudo
ansible-playbook playbook.yml --ask-become-pass --become

# Run Playbook as sudo user janedoe and ask for her password
ansible-playbook playbook.yml --become --become-user=janedoe --ask-become-pass

```
```
ansible-playbook playbook.yml --extra-vars="node_apps_location=/usr/local/opt/node" --limit 192.168.60.4

# Navigate to 192.168.60.4 in a browser to see working hello world or:
curl 192.168.60.4
```
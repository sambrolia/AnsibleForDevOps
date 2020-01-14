Simple playbook which sets up NTP is used to provision a VM created with vagrant.

Code Vagrantfile to add the provisioning:

```
  # Provisioning configuration for Ansible.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
```
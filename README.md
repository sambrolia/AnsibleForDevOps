# AnsibleForDevOps
Code and scripts created while working through the book "Ansible for DevOps" by Jeff Geerling  

# Set up
Install Vagrant and virtualbox on windows  
Install Vagrant (same version as windows) in wsl  
Install ansible in wsl  

Add following to ~/.bashrc in wsl:  
Note - "/c" for me is usually "/mnt/c"  

```
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
export PATH=$PATH:/c/Windows/System32
export PATH="$PATH:/c/Program Files/Oracle/VirtualBox"
```

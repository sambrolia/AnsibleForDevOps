```
# For human readable output
export ANSIBLE_STDOUT_CALLBACK=debug
```

```
ansible multi -a "date"  
ansible [host-or-group] -m setup # Get all ansible environment facts  
ansible multi -b -m yum -a "name=ntp state=present"
ansible multi -b -m service -a "name=ntpd state=started enabled=yes"  

ansible multi -b -a "service ntpd stop"  
ansible multi -b -a "ntpdate -q 0.rhel.pool.ntp.org"  
ansible multi -b -a "service ntpd start"  
```

```
# install django on app machines
ansible app -b -m yum -a "name=MySQL-python state=present"
ansible app -b -m yum -a "name=python-setuptools state=present"
ansible app -b -m easy_install -a "name=django<2 state=present"

# test its installed
ansible app -a "python -c '\
import django; \
print django.get_version()'"
```

```
# install MariaDB on the db machines
ansible db -b -m yum -a "name=mariadb-server state=present"
ansible db -b -m service -a "name=mariadb state=started enabled=yes"

# configure the firewall to allow acces on port 3306 for mariadb
ansible db -b -a "iptables -F"
ansible db -b -a "iptables -A INPUT -s 192.168.60.0/24 -p tcp -m tcp --dport 3306 -j ACCEPT"

# Set up the database
ansible db -b -m yum -a "name=MySQL-python state=present"
ansible db -b -m mysql_user -a "name=django host=% password=12345 priv=*.*:ALL state=present"

```


```
# check ntp status and restart the particular machine which had issues
ansible app -b -a "service ntpd status"  

ansible app -b -a "service ntpd restart" --limit "192.168.60.4"
ansible app -b -a "service ntpd restart" --limit "*.4"
ansible app -b -a "service ntpd restart" --limit ~".*\.4"
```

```
# Add an admin group on app servers
ansible app -b -m group -a "name=admin state=present"

# Add a user to the group (with or without ssh key)
ansible app -b -m user -a "name=johndoe group=admin createhome=yes"
ansible app -b -m user -a "name=johndoe group=admin createhome=yes generate_ssh_key=yes"

# Remove the user
ansible app -b -m user -a "name=johndoe state=absent remove=yes"
```

```
# Manage packages
ansible app -b -m package -a "name=git state=present"
```

```
# Get information about a file
ansible multi -m stat -a "path=/etc/environment"

# Copy a file to the servers
ansible multi -m copy -a "src=/etc/hosts dest=/tmp/hosts"

# Retrive a file from the servers and put them in /tmp/{IP_ADDRESS}/etc/hosts
ansible multi -b -m fetch -a "src=/etc/hosts dest=/tmp"

# Retrive a file from the servers and put them in /tmp/
ansible multi -b -m fetch -a "src=/etc/hosts dest=/tmp/ flat=yes"

# Create directory
ansible multi -m file -a "dest=/tmp/test mode=644 state=directory"

# Create symlink
ansible multi -m file -a "src=/src/file dest=/dest/symlink state=link"

# Delete file directory or symlink
ansible multi -m file -a "dest=/tmp/test state=absent"
```

```
# Run asynchronously
ansible multi -b -B 3600 -P 0 -a "yum -y update"

# Veiw progress of job (use jid from previous commands output)
ansible multi -b -m async_status -a "jid=729193165734.11275"
```

```
# Veiw tail of log file
ansible multi -b -a "tail /var/log/messages"

# Count ansible commands
ansible multi -b -m shell -a "tail /var/log/messages | grep ansible-command | wc -l"
```
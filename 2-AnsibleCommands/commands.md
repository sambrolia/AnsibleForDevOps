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
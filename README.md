# How to Install Nagios 4 (Monitoring Server) on CentOS/RHEL 7/6
```
yum install httpd php php-cli gcc unzip wget glibc glibc-common gd gd-devel net-snmp
service httpd start
useradd nagios
passwd nagios
groupadd nagcmd
usermod -a -G nagcmd nagios
usermod -a -G nagcmd apache
```
##  Install Nagios Core Service
```
cd /opt/
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.3.tar.gz
tar xzf nagios-4.4.3.tar.gz
cd nagios-4.4.3
./configure --with-command-group=nagcmd
make all
make install
make install-init
make install-daemoninit
make install-config
make install-commandmode
make install-exfoliation
```
###  setup Apache configuration for Nagios installation
```
make install-webconf
Configure Apache Authentication
htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin ----->admin passwd for http://10.0.56.66/nagios/
service httpd restart
```
##  Install Nagios Plugins
```
cd /opt
wget http://nagios-plugins.org/download/nagios-plugins-2.2.1.tar.gz
tar xzf nagios-plugins-2.2.1.tar.gz
cd nagios-plugins-2.2.1
```
install nagios plugins
```
./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
make install
```
## Verify and Start Nagios
- /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
- service nagios start
# Access Nagios in Web Browser

Nagios creates its own apache configuration file /etc/httpd/conf.d/nagios.conf. There are no need to make any changes to it. Simply open below url in browser
- http://10.0.56.66/
- http://10.0.56.66/nagios/   ---->username--->nagiosadmin,, passwd---->admin
- the default port number is 5666

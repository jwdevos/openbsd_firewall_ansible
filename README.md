# openbsd_firewall_ansible
Build a basic OpenBSD firewall with Ansible

**to do**
* test dhcpd config
* stop and start dhcpd if needed
* start dhcpd on boot
* 
* start pf if needed and config is good
* reload pf config if needed and config is good
* start pf on boot
* 
* test firewall
* reboot
* test firewall again
* 
* check for state in playbooks, should only be allowed in vars

**project explanation**
* pf template breaks with multiple interfaces as external
* tested on OpenBSD 6.2

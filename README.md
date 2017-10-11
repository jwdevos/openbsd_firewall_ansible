# openbsd_firewall_ansible
Build a basic OpenBSD firewall with Ansible

**to do**
* test pf config
* (re)start services if shit is good _and_ changed
* test
* reboot
* test again
* only run ntpd -s if needed
* check for state in playbooks, should only be allowed in vars

**project explanation**
* pf template breaks with multiple interfaces as external

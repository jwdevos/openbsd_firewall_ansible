# openbsd_firewall_ansible
Build a basic OpenBSD firewall with Ansible

**project explanation**  
* pf template breaks with multiple interfaces as external
* tested on OpenBSD 6.2
* ssh allow rule niet in productie nemen


**How to use**  
Start with a fresh install of OpenBSD reachable via SSH as root on an IPv4 address. Have this Ansible project ready on another host that can reach the OpenBSD box. Just run the two following playbooks from the main project directory (./openbsd_firewall_ansible/):
```
ansible-playbook bootstrap.yml -i inventory --ask-pass
ansible-playbook play_setup.yml -i inventory --ask-pass
```

# openbsd_firewall_ansible
Build a basic OpenBSD firewall with Ansible

fully bla config via vars geen state in playbooks en templates

**project explanation**  
* pf template breaks with multiple interfaces as external
* tested on OpenBSD 6.2
* ssh allow rule niet in productie nemen

**How to use**  
Start with a fresh install of OpenBSD reachable via SSH as root on an IPv4 address. Have this Ansible project ready on another host that can reach the OpenBSD box.

This project should work with the defaults right away but you should set all your config by editing the host_vars.

Just run the two following playbooks from the main project directory (./openbsd_firewall_ansible/):
```
ansible-playbook bootstrap.yml -i inventory --ask-pass
ansible-playbook play_setup.yml -i inventory --ask-pass
```

**What's happening?**

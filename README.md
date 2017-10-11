# openbsd_firewall_ansible  
This Ansible project is used to deploy and manage an OpenBSD firewall running pf and dhcpd. The playbooks deploy a running firewall taking nothing more than a fresh install of OpenBSD. The project produces a minimum viable product to demonstrate a working firewall. It is intended for demonstration purposes but can be taken freely to suit your own needs. The cool thing is that all of the unique configuration is in the files under host_vars. That means you can easily make configuration changes to a running box and reload only the services that were affected. For pf, the firewall keeps running if you just reload the configuration.

**How to use**  
Start with a fresh install of OpenBSD reachable via SSH as root on an IPv4 address. Have this Ansible project ready on another host that can reach the OpenBSD box.

This project should work with the defaults right away but you should set all your config by editing the host_vars.

Just run the two following playbooks from the main project directory (./openbsd_firewall_ansible/):
```
ansible-playbook bootstrap.yml -i inventory --ask-pass
ansible-playbook play_setup.yml -i inventory --ask-pass
```

**What's happening?**  
bla

**Some notes**  
* For 9 out of 10 use cases there is only going to be one external interface. This project was coded for that use case only. Adding more than one interface variable set to external might harm the playbook execution or the functionality of the running firewall
pf template breaks with multiple interfaces as external
* The code was tested on OpenBSD 6.2
* There is a rule in pf allowing ssh connections to the external interface. This rule is used for testing and should not be loaded for production systems without further measures

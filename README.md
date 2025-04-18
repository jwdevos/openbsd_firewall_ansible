**-- this repo will be archived and moved to https://codeberg.org/jwdevos/openbsd_firewall_ansible --**

# openbsd_firewall_ansible  
This Ansible project is used to deploy and manage an OpenBSD firewall running pf and dhcpd. The playbooks deploy a running firewall taking nothing more than a fresh install of OpenBSD. The playbooks produce a minimum viable product to demonstrate a working firewall. They are intended for demonstration purposes but can be taken freely to suit your own needs. The cool thing is that all of the unique configuration is in the variables under host_vars. That means you can easily make configuration changes to a running box and reload only the services that were affected. With pf, the firewall keeps running if you just reload the configuration.

**How to use**  
Start with a fresh install of OpenBSD reachable via SSH as root on an IPv4 address. You'll need at least two network interfaces. Have this Ansible project ready on another host that can reach the OpenBSD box.

This project should work with the defaults right away but you should set all your config by editing the host_vars. You can set the IP address of the target host in the /host_vars/obsd-test/ansible.yml file.

Just run the two following playbooks from the main project directory (./openbsd_firewall_ansible/):
```
ansible-playbook bootstrap.yml -i inventory --ask-pass
ansible-playbook play_setup.yml -i inventory --ask-pass
```
The play_setup.yml playbook can also be used for making changes after the initial deployment. The intention is to do all of the management of the firewall with the playbooks.

**What's happening?**  
OpenBSD doesn't have Python by default. The bootstrap playbook makes sure that package managent is configured on the host and that Python is available, installing it if necessary.  
The setup playbook actually calls an ansible role taking care of lots of things. It takes the content of the host_vars and makes sure following things get done:
1. Set the system hostname to the correct value if necessary
2. Make sure interface configuration files are set to the correct state
3. Configure the rc.conf.local file for dhcpd and virtual tools if necessary
4. Restart netwoking if relevant configuration was changed
5. Configure dhcpd and make sure the service is started
6. Configure time
7. Configure IP forwarding
8. Configure the pf firewall, testing the configuration file and reloading the firewall if relevant configuration was changed

Most of the items in the list above rely on the Jinja2 templates in the templates-directory. These templates make use of the content of the host_vars.

**Some notes**  
* Additional firewall rules have to be added in the template file at this moment. The intention is to look into generating the rules, taking the content from host_vars
* For 9 out of 10 use cases there is only going to be one external interface. This project was coded for that use case only. Adding more than one interface variable set to external might harm the playbook execution or the functionality of the running firewall
pf template breaks with multiple interfaces as external
* The code was tested on OpenBSD 6.2
* There is a rule in pf allowing ssh connections to the external interface. This rule is used for testing and should not be loaded for production systems without further measures

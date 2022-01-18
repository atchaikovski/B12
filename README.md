# README #

This homework is for SkillsFactory B12.

### What is this repository for? ###

* Deploying Jenkins and 2 agents, then 2 VMs (prod and stage). 
* NGINX as proxy added, https to it, then http to jenkins
* --- Jenkins should have access to all VMs (not yet)
* Jenkins currently starts without setup, admin user gets created auto
* plugins get copied and installed auto
* need to connect 2 agents automatically
* all things preferrably should have been installed automatically by ansible or similar
* making some jobs to show that Jenkins is fully functional and capable
* Version 0.3

### How do I get set up? ###

* this runs under vagrant and ESXi provider
* just copy it and edit hosts file (inventory)
* and make sure you configured ESXi access (credentials/IPs etc.)
* make sure you have all those keys populated in your system (id_rsa) and secrets/ directory with the keys/params as it was removed from my repo
* then vagrant up

### Who do I talk to? ###

* Alex Tchaikovski (alex@tchaikovski.net) 

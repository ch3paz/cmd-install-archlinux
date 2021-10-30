# Description

Installs and configures an Archlinux-machine as an UEFI-install.

This is an stripped down playbook which i previously have written to
automagic create+boot+install an KVM-host on libvirt.

# Basic usage

The idea here is:
* to boot an archiso
* install ansible in booted the live system to run the playbook
* clone this playbook from your $VCS (Gitlab, Bitbucket, Github...)
* copy vars_example.yml to vars.yml (or create a different copy and link it to vars.yml)
* run the playbook, let it do all the anoying stuff and be happy with an new Archlinux-machine (see "Example" below)

# Prerequisites

* Take a look in the vars.yml, adapt it, and save your config to a new file (e.g.: vars_newhostname.yml)
* Link this vars-file to vars.yml, e.g.: `ln -s vars_vars_newhostname.yml vars.yml`
* Run the playbook (see "Example" below)

# Example

~~~
ansible-playbook -i inventory main.yml -l cubox -K
~~~

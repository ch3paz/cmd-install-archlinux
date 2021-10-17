# Description

Creates, installs, boots and configures an Archlinux-machine on an KVM host.

# Prerequisites

* Take a look in the vars.yml, adapt it and save your config to a new file (e.g.: vars_newhostname.yml)
* An modified arch-iso is needed with sshd and rootlogin enabled.

# Example

~~~
ansible-playbook -i ../ansible-inventorys/inventory main.yml -e "vars_files=vars_newhostname.yml, initial_root_pw_vm=CHANGEME, initial_root_pw_iso=CHANGEME" -l cubox --check
~~~

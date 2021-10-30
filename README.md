# Description

Installs and configures an Archlinux-machine as an UEFI-install.

This is an stripped down playbook which i previously have written to
automagic create+boot+install an KVM-host on libvirt.

It will _kill everything_ on the device noted in `disk_blockdevice` in the 'vars.yml`!

# Basic usage

The idea here is:
* to boot an archiso
* install ansible in booted the live system to run the playbook
* clone this playbook from your $VCS (Gitlab, Bitbucket, Github...)
* copy vars_example.yml to vars.yml (or create a different copy and link it to vars.yml)
* run the playbook, let it do all the anoying stuff and be happy with an new Archlinux-machine (see "Example" below)

# Prerequisites

* Take a look in the vars.yml, adapt it (maybe save your config to a new file (e.g.: vars_newhostname.yml) and link this vars-file to vars.yml, e.g.: `ln -s vars_newhostname.yml vars.yml`
* Run the playbook (see "Example" below)

# Example

To make copy&paste easier change roots password and SSH into the booted archiso:

~~~
root@archiso ~ # passwd
New password: 
Retype new password: 
passwd: password updated successfully
~~~

then

~~~
# If 'archiso' doens't work in your network, use the ip of the livesystem
ssh root@archiso
~~~

In the archiso-environment run:

~~~
# Resize / as it is too small for ansible+sshpass+git
mount -o remount,size=2G /run/archiso/cowspace

# Install ansible+sshpass+git 
pacman -Sy && pacman -S ansible sshpass git --noconfirm

# Clone the playbook, adapt the URL to your needs
git clone https://gitlab.chepnet.lan/chepaz/cmd-install-archlinux-onkvm.git

# Run the playbook
cd cmd-install-archlinux-onkvm && ansible-playbook -i inventory -l archiso main.yml -k
~~~

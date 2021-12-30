# Description

Installs and configures an Archlinux-machine as UEFI-install.

This is an stripped down playbook which i previously had written to automagic create+boot+install an KVM-host on libvirt. The intention was to fire up Archlinux very quick, very dirty, for testing purposes.

**Warning:** It will **_kill everything_** on the device noted in `disk_blockdevice` in the `vars.yml`

## Remark

* Defaults to german locale, if you need to change the locale you have to adapt the corresponding lines in the `main.yml`
* Some packages, which i prefere for an basic-install, are installed also. See `main.yml` for details
* The mirrorlist needs to be adapted to your location

# Basic usage

The idea here is:
* Boot an archiso
* Install needed tooling into the booted live system to run the playbook
* Clone this playbook from your $VCS (Gitlab, Bitbucket, Github...)
* Adapt vars.yml
* Run the playbook (let it do all the boring stuff and be happy with your new Archlinux-machine)

# Example

## Boot the archiso

Just boot archiso

## SSH into archiso

To make copy & paste easier change the root password and SSH into the booted archiso:

~~~
root@archiso ~ # passwd
New password: 
Retype new password: 
passwd: password updated successfully
~~~

then, from your client, ssh into archiso:

~~~
ssh root@archiso
~~~

**Hint:** If the hostname 'archiso' doesn't work in your network, use the ip of the livesystem

## In the archiso-environment run:

### Resize / as it is too small for ansible+sshpass+git

~~~
mount -o remount,size=2G /run/archiso/cowspace
~~~

### Install ansible+sshpass+git 
~~~
pacman -Sy && pacman -S ansible sshpass git --noconfirm
~~~

### Clone the playbook, adapt the URL to your needs
~~~
git clone https://github.com/ch3paz/cmd-install-archlinux.git
~~~

### Prerequisites

Cd into the cloned dir

~~~
cd cmd-install-archlinux
~~~

and

* Modify `main.yml` if you need to change locale or packages (or even more ;) )
* Modify `vars.yml`, adapt it. Maybe save your config to a new file, e.g. `vars_newhostname.yml`, and link this file to `vars.yml` --> `ln -s vars_newhostname.yml vars.yml`

### Run the playbook
~~~
export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook -i inventory -l archiso main.yml -k
~~~

# Troubleshooting

In case you see errors like `ImportError: No module named ansible` then the packages on the iso are outdated for ansible or the iso is to old.

You may try to update the packages with `pacman -Syu` but this might not work in all cases as this also updates the kernel.

If this doesn't help, try the latest install-iso or build your own one with archiso and integrate ansible, git and sshpass.
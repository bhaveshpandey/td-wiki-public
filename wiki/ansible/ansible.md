# Ansible

## Installation

We can install Ansible on ubuntu as following.

```shell

sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu


Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code.

**Ansible** can be used to execute batch commands over a large number of hosts/machines, as long as they are accessible via **SSH**.

## Prerequisites

To be able to authenticate using ssh password with the host machines, we also need to install a package called `sshpass`
On Ubuntu, it can be installed with

```shell

sudo apt install sshpass -y
```

## Navigating Ansible documentation from CLI

If you remember anything from this, remember this:


Show documentation for ansible
```shell

ansible-doc -l
```

Show documentation on a specific module

```shell

ansible-doc shell
```

**NOTE**
```text
Anything in the help documentation for modules which is prefixed with = is a mandatory argument.
```


## Adhoc commands

Adhoc commands are useful for the users to quickly probe the hosts, run tests etc. I found it useful to even use adhoc commands to batch reboot multiple hosts efficiently.

* [Adhoc Commands](adhoc.md)

## Playbooks

Playbooks allow users to execute multiple tasks on several hosts in an efficient manner.

* [Playbook](playbook.md)


## Resources

* [Complete Ansible Course](https://www.youtube.com/watch?v=KuiAiUyuDY4&list=PLnFWJCugpwfzTlIJ-JtuATD2MBBD7_m3u)
* [Ansible Google Groups](https://groups.google.com/g/ansible-project)
* [Configure Ubuntu Server setup using Ansible Playbook](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-18-04)
* [Sudo in Ansible using become](https://www.middlewareinventory.com/blog/ansible-sudo-ansible-become-example/)
* [Setting up SSH Password for ansible authentication](https://linuxhint.com/how_to_use_sshpass_to_login_for_ansible/)
* [Configuration Variables Available](https://docs.ansible.com/ansible/2.3/intro_configuration.html#remote-tmp)

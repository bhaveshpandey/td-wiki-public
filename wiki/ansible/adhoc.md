# Adhoc commands

For the examples below, we are using a very bare-bones inventory file. The contents of this file are as follows.

```text

[rpi]
foo
bar

[all:vars]
ansible_user=<USER_NAME>
ansible_ssh_pass=<USER_PASS>
become=yes
become_user=root
```


### Ping

Following command using the `ping` module to communicate with the `london` host from the specified `inventory` file.

```shell

ansible all --inventory=inventory -m ping
```

### Reboot

Rebooting a host/machine remotely using Ansible using `reboot` module.

```shell

ansible all --inventory=inventory -m reboot -a reboot_timeout=3600 -u atoi -b -K
```

where:
* -a: flag to specify arguments to the reboot module.
* -reboot_timeout: time to wait after reboot in seconds. 3600 means 60mins.
* -u: remote user
* -b: become root user
* -K: ask for password. Without this flag, ansible will give an error.

### Creating Users

We can create users on host machines easily as follows.

```shell

ansible all --inventory=inventory -m user -a "name=foobar password=12345"
```
Looking at the documentation for the user module by running  following command in the shell.

```shell

ansible-doc user
```

As can be seen in the documentation for the `user` module, `name` is a mandatory argument.

### Installing packages

We can also install packages using Adhoc commands using 2 different approaches.
1. Options
2. Modules

**Using Options**

```shell

ansible all --inventory=inventory -a "apt install redis-server redis-tools" -b -K
ansible all --inventory=inventory -a "apt remove redis-server redis-tools" -b -K
```

**Using modules**

```shell

ansible-doc apt
ansible all --inventory=inventory -m apt -a "name=redis-server state=present" -b -K
ansible all --inventory=inventory -m apt -a "name-redis-server state=absent" -b -K
```


## Resources

* [Adhoc command examples](https://www.middlewareinventory.com/blog/ansible-ad-hoc-commands/#What_is_Ansible_ad_hoc_commands)

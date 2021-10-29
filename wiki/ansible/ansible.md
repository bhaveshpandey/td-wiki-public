# Ansible

Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code.

**Ansible** can be used to execute batch commands over a large number of hosts/machines, as long as they are accessible via **SSH**.

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

**Anything in the help documentation for modules which is prefixed with `=` is a mandatory argument.**


* [Adhoc Commands](adhoc.md)
* [Playbook](playbook.md)

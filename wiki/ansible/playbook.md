# Playbook

Ansible Playbooks are a set of instructions to be followed when executing tasks. It usually is in form of a YAML file.
## Example

For the following examples we will be using a bare-bones playbook file which will have contents as below.

**testplay.yml**
```yaml

---
# This playbook will be executed on hosts which are included in the FooGoup
- hosts: FooGroup
  tasks:
    # This shows how we can use apt module to install packages
    - name: Install redis-server
      apt: name=redis-server state=latest
      become: true

    # This shows how we can start/stop services
    - name: Start redis server
      service: name=redis-server state=restarted
      become: true

    - name: Install cypher lint
      apt: name=cypher-lint state=present
      become: true

    - name: Example showing how to pass arguments within playbook from CLI
      shell: |
        echo "{{some_var_foo}}: \{\{ ansible_eth0.ipv4.address }}" > ~/foo.txt
        exit 0
```


**Note:**

We can access the current host's IP address, using `{ { ansible_eth0.ipv4.address} }` as shown in the above example.


We will be using the above playbook in conjunction with following inventory file.

**inventory**
```text

[FooGroup]
foo
bar

[all:vars]
ansible_user=some_user_blah
ansible_ssh_pass=<USER_PASS>
ansible_become_pass=<SUDO_PASS>
become=yes
become_user=root

```

A more secure version of this inventory can be seen below in the **Passing arguments to Playbook**.

### Executing Playbooks

We can run the above playbook using `ansible-playbook` command. However, before executing any plays, its good practice to syntax check the playbook. We can do this as follows.

```shell

ansible-playbook --inventory=inventory testplay.yml --syntax-check
```

If the syntax is good, it would simply return the name of the playbook. In which case, we can go ahead and run the playbook as follows.

```shell

ansible-playbook --inventory=inventory testplay.yml
```

The above command will be executed on all the hosts defined in the inventory by default. However, we can also over-ride this by supplying the `limit` argument as follows.

```shell

ansible-playbook --inventory=inventory testplay.yml --limit=foo
```

The above command will execute the specified playbook `testplay.yml` only on the host named `foo`

**Passing arguments to Playbook**

We can pass arguments to the Ansible playbook as follows.

```shell

ansible-playbook --inventory=inventory testplay.yml --extra-vars "some_var_foo='hello there! wassup?'"
```

As can be seen above, we are passing `some_var_foo` as `extra-vars` which is then accessed from within the **Playbook** using jinja notation `"{{some_var_foo}}"`.

Using the above technique, we can also secure our playbooks by passing the passwords as extra-vars

```shell

...

[all:vars]
ansible_user=some_user_blah
ansible_ssh_pass="{{ssh_pass}}"
ansible_become_pass="{{sudo_pass}}"
become=yes
become_user=root
```

And ansible-playbook can now be run by supplying ssh_pass as an extra-vars

```shell

ansible-playbook --inventory=inventory testplay.yml --extra-vars="ssh_pass=<SSH_PASS> sudo_pass=<SUDO_PASS>"
```

Or better yet, by using the `-K` flag (ask become password) which allows users to interactively supply a password. But for this to work, we will need to remove the `ansible_become_pass="{{sudo_pass}}"` line from the inventory.

```shell

ansible-playbook --inventory=inventory testplay.yml --extra-vars="ssh_pass=<SSH_PASS>" -K
```

## [Sample Playbooks](playbooks/playbooks.md)

## Resources

* [Configure Ubuntu Server setup using Ansible Playbook](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-18-04)
* [Shell examples](https://www.middlewareinventory.com/blog/ansible-shell-examples/)

# K3S

As root do following:

1. sudo iptables -F
2. sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
3. reboot

There seem to be some issues with the firmware. To fix these, add following to the line in `/boot/firmware/cmdline.txt` file.

    `cgroup_memory=1 cgroup_enable=memory`

We can verify whether this has taken effect or not as shown below:

```shell

cat /proc/cmdline | grep cgroup
```

If the above steps are not followed, running k3s server will complain about not finding the `cgroup` on the host.


Installing K3S

As root do:

1. curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -
2. Now a K3S server can be run by simply executing as root (sudo su -)
   `k3s server`

Installation of the master node is finished.

To install k3s on a worker node, follow all the above steps. However we also need a token from the master node.
---
NOTE:

Its important to repeat steps 1-3 outlined at the top.

---

```shell

cat /var/lib/rancher/k3s/server/node-token
```

curl -sfL https://get.k3s.io | K3S_TOKEN="TOKEN_FROM_MASTER_NODE" K3S_URL="https://IP_ADDRESS_OF_MASTER" K3S_NODE_NAME="raspi-worker1" sh -


## Official Rancher Installation Guide

* [k3s installation](https://www.rancher.co.jp/docs/k3s/latest/en/running/)

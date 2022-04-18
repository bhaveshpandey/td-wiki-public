# K3S

## Installation

**Installing on master node**

```shell
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" K3S_NODE_NAME="grid-rpi4-master1" sh -s -
cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
export KUBECONFIG=~/.kube/config
```

To access the cluster from another machine, copy the `KUBECONFIG` to the machine and change the
`IP address` to the master nodes `IP address`.

We can use `scp` for this, as follows:

`scp <USER>@HOST:~/.kube/config ~/.kube/config`

**Installing without Traefik**

`curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" K3S_NODE_NAME="grid-rpi4-master1" sh -s - server --cluster-init --disable traefik --disable servicelb`


Installing on another machine and joining the master

`curl -sfL https://get.k3s.io | K3S_TOKENN="<K3S_TOKEN>" K3S_URL="https://172.0.0.1:6443" K3S_NODE_NAME="grid-rpi4-worker1" sh -`


## Restart a node

Restarting nodes in K3S is not as easy as in K3D.

```shell

kubectl drain nodes <NODE-NAME>

# Optionally following might be required for ignoring daemon sets
kubectl drain nodes <NODE-NAME> --ignore-daemonsets --delete-emptydir-data

# Optionally might need to delete the node
kubectl delete nodes <NODE-NAME>

# Restart k3s master (sometimes)
sudo systemctl k3s restart
```

I have noticed sometimes when updating the nodes (re-installing a fresh OS etc), we need to either restart the node or cluster (dont know for sure yet).


## Importing local Docker images into K3S

1. Save the docker image as a tarball.

```shell

docker save --output ~/foo.0.1.tar test/foo:0.1
```

2. Import the image into the node/worker machine.

```shell

sudo k3s ctr images import ~/foo.0.1.tar
```

The above command will import the image into the node (similar to k3d image import)

3. Verify that the image is indeed imported.

```shell

sudo k3s ctr images list
```


## References

* [Raspberry Pi homelab with Kubernetes - Metallb, Ansible, Helm](https://fredrickb.com/2021/08/22/recreating-the-raspberry-pi-homelab-with-kubernetes/)

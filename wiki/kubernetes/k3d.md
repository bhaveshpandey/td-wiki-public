# K3D

Kubernetes in a Docker container.

## Creating clusters

```shell

k3d cluster create foo-cluster -s 1 -a 4
```

The above command shows how to create a cluster named `foo-cluster` with:
* servers: 1
* agents: 4

We can also specify the image we want to use for creation of our clusters as shown below.

```shell

k3d cluster create foo-cluster --image rancher/k3s:v1.20.4-k3s1
```

We can list all the clusters using the list subcommand as follows.

```shell

k3d cluster list
```


## Deleting clusters

```shell

k3d cluster delete foo-cluster
```


## Config file

Running commands in cli to interact with k3d is useful for quick probing and tests however being able to define all the configuration in a config file makes things `reusable`, `deterministic` and `modular`.

```yaml

kind: Simple
apiVersion: k3d.io/v1alpha2
name: foo-cluster
image: rancher/k3s:v1.20.4-k3s1
servers: 2
agents: 4

ports:
- port: 80:80
  nodeFilters:
  - loadBalancer

# options:
#   k3s:
```

Now we can create clusters using this config file as shown below.

```shell

k3d cluster create --config /path/to/config.yml
```

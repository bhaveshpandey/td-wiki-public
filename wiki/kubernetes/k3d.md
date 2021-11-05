# K3D

Kubernetes (K3S) in a Docker container.

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
k3d node list
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
```

Now we can create clusters using this config file as shown below.

```shell

k3d cluster create --config /path/to/config.yml
```

## Adding nodes

We can also add nodes to an already existing cluster with ease. Below is a quick example showing this.

```shell

k3d node create --help
k3d node create new_node_name -c CLUSTER_NAME -r NUM_AGENTS --role agent
```

[K3D]() allows us to create and manage multiple clusters locally with relative ease. However when using `kubectl` to interact with these clusters, it will always communicate with the last cluster which was created. If we need to communicate with another cluster, we will need to explicitly specify the context. This is shown below.

```shell

# Get a list of all available contexts
kubectl config get-contexts

# Explicitly ask kubectl to communicate with another cluster
kubectl config use-context OTHER_CONTEXT_NAME

# Get config file contents for a cluster
k3d kubeconfig get NAME_OF_CLUSTER
```

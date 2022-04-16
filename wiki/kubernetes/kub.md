# Kubernetes

Kubernetes is a container orchastration engine.

## Cheat Sheet

[Kubernetes cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#viewing-finding-resources)


## Key Concepts

**Following is an illustration of a basic K8s hierarchy**

Cluster
    |__
    Worker Node
        |__
            Pod
            |__
                Container
                    |__
                        Application

* Master Node (Control Plane)
* Worker Node
* Pod - Smallest unit of a K8s cluster.
* Container
* Deployment
* Replica Sets
* Service
* Namespace
* CRD (Custom Resource Definition)
* Persistent Volume/Volume Claim
* API Service
* Controller
* Data Store
* Scheduler
* Kubelet
* Kube Proxy


## kubectl

* [Installation](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management)

### Autocompletion

A few extra steps are required for kubectl to work seamlessly with ZSH/BASH autocompletion. Lets have a look at each of these below.

**ZSH**

For all my ZSH needs, I lean quite heavily on [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh). This is fairly trivial to setup for ZSH using **oh-my-zsh**.

```shell

plugins = (
    kubectl
)
```
As shown above, we simply need to specify `kubectl` and `k3d` for adding support for autocompletion in `ZSH`.


**Bash**

Setting up autocompletion for bash involves a few more steps [outlined in the documentation](https://kubernetes.io/docs/tasks/tools/included/optional-kubectl-configs-bash-linux/).

For brevity, I will document these briefly here.

1. Make sure `bash-completion` is installed.
    ```shell

    sudo apt install bash-completion
    ```
2. Source completion script in your bashrc.
    ```shell

    echo 'source <(kubectl completion bash)' >>~/.bashrc
    ```
3. Add the completion script to `/etc/bash_completion.d` dir.
    ```

    kubectl completion bash >/etc/bash_completion.d/kubectl
    ```

Autocompletion for kubectl should now be available on BASH.


## Misc

```shell

kubectl get pods -A

kubectl get pods -Ao wide

kubectl get nodes

kubectl config get-contexts

kubectl config use-context NAME_OF_CONTEXT_TO_SWITCH_TO

# Get the config map for traefik deployment
kubectl -n kube-system describe deploy traefik

# Get the config map
kubectl -n kube-system get cm

# Tainting nodes to avoid deploying workloads on master nodes
kubectl taint nodes <MASTER-NODE-NAME> node-role.kubernetes.io/master=true:NoSchedule

```

## Creating namespaces

```shell

kubectl create namespace dev
kubectl create namespace staging
kubectl create namespace prod
```

We can list all the namespaces as follows.

```shell

kubectl get namespaces

```

## Force clearing PV, PVC

Sometimes deleting `pv,pvc` using `kubectl delete` doesn't remove the volumes or the claims. This can be forced by setting the `finalizers` to `null` explicitly as follows.

```shell

kubectl patch pvc <PVC_NAME> -p '{"metadata":{"finalizers":null}}'
kubectl patch pv <PV_NAME> -p '{"metadata":{"finalizers":null}}'
```


## Role Based Access Control

* [RBAC](rbac.md)

## K3S

* [K3S](k3s.md)

## K3D

* [K3D](k3d.md)

# Kubernetes

Kubernetes is a container orchastration engine.

## kubectl

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

## Role Based Access Control

* [RBAC](rbac.md)

## K3S

* [K3S](k3s.md)

## K3D

* [K3D](k3d.md)

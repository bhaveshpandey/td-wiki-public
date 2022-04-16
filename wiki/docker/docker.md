# Docker

## Installation

### OSX

```shell

# Following will install docker-desktop and cli. This seems to be the easiest way I could find to install Docker on OSX
brew install --cask docker
```

* [On OSX](https://www.cprime.com/resources/blog/docker-on-mac-with-homebrew-a-step-by-step-tutorial/)

### Linux

Installation on Linux is fairly straight-forward. Follow the guide below.

* [Install instructions on linux](https://docs.docker.com/engine/install/ubuntu/)
* [Install instructions for Linux Mint](https://www.how2shout.com/linux/2-ways-to-install-docker-engine-on-linux-mint/)

Post install steps

* [Manage Docker as a non-root user](https://docs.docker.com/engine/install/linux-postinstall/)

## Common commands

Some of the most common commands for querying docker images, containers etc are listed as follows.

```shell

docker image ls
docker container ls
docker ps
docker rm
docker pull
docker push

docker inspect <CONTAINER_ID/CONTAINER_NAME>
docker logs <CONTAINER_ID>
docker logs -f <CONTAINER_ID>
docker stats <CONTAINER_ID>

docker start <CONTAINER_ID>
docker stop <CONTAINER_ID>
docker restart <CONTAINER_ID>

docker build -t <TAG_NAME> .
docker run <IMAGE_NAME>

# Passing Env vars to docker container and also defining an explicit name of the container.
# Note the name HAS to be unique
docker run -it --name="NEW_CONTAINER_NAME" -e NEO4J_PASSWORD 'SomeSecureShit' <IMAGE_TAG_TO_RUN> <COMMAND>

# Run a container in detached mode
docker run -d

# List all dangling images
docker image ls --filter=dangling

# Create another image with changes done in a source image interactively
docker commit SRC_IMAGE <tag>

# Show history of an image
docker image history <IMAGE_TAG>

# Inspect docker images
docker image inspect <IMAGE_TAG>
```

## Bare-bones example

```dockerfile

FROM alpine:latest

RUN apk update

RUN apk install vim

```

The above example shows a `Dockerfile` which acts as a blueprint for creating images. We can now create an image as shown below.

```shell

docker build -t 'foo-something:0.1'
```

A docker container can now be run using the above image as follows:

```shell

docker run foo-something:0.1
```

This would create an instance of the `foo-something:0.1` image which is called a `container`.

We can also run this in interactive mode as follows:

```shell

docker run -it --rm foo-something:0.1
```

## Volume Mapping

Often times we require access to persistent data within our docker containers. This can be achieved by mounting volumes with the `-v` flag as shown below.

```shell

docker run -it --rm -v `PATH/TO/MOUNT`:/MOUNT_NAME 'foo-something:0.1'
```

**Where:**

* `PATH/TO/MOUNT` is the directory we want to make accessible to docker container

* `MOUNT_NAME` is the directory it is mapped to within the docker container.


## Port Mapping

```shell

# This will have following format
# docker run -h <HOST_NAME> -p <LOCALHOST_PORT/DOCKER_SERVER_PORT>:<CONTAINER_PORT> <IMAGE_TAG_TO_RUN>

docker run -h funky_panda -p 8000:80 blah:0.2
```


## Running containers

We can run a container in a few different ways.

### Interactive mode (with terminal)

```shell

docker run -it <IMAGE_TAG>
```

### Interactive Detached mode

```shell

docker run -itd <IMAGE_TAG>
```

In this mode the container stays up and we can interact with it and send commands to it as follows.

```shell

# These commands can be in following format
# docker exec <CONTAINER_ID> <COMMAND>

# The following command will execute the ls -lrth command in the active container with specified Container ID
docker exec 213hdsu3jmbj2b1 ls -lrth
```


## Inspecting Running Containers


Specifying a filter to extract required data from the inspect command.

```shell

docker inspect -f "{{.Config.Env}}" <CONTAINER_ID/CONTAINER_NAME>
docker inspect -f "{{.NetworkSettings}}" wizardly_me
docker inspect -f "{{.State.Status}}" wizardly_me
docker inspect -f "{{.Config.Hostname}}" wizardly_me
docker inspect -f "{{.Mounts}}" wizardly_me
docker inspect -f "{{.State.Pid}}" wizardly_me

# Looping over values in the map
docker inspect -f "{{range .NetworkSettings.Networks}} {{.IPAddress}}  {{end}}" wizardly_ramanujan

# Display IPAddress with a label of IP:
docker inspect -f "{{range .NetworkSettings.Networks}} IP: {{.IPAddress}}  {{end}}" wizardly_ramanujan

docker inspect -f "{{range .NetworkSettings.Networks}} MAC: {{.MacAddress}} IP: {{.IPAddress}}  {{end}}" wizardly_ramanujan
```

The above command will extract the Config.Env from the json data returned by inspect command.


## Running Container with an Enntrypoint override

This is quite often required to interactively see what the internals of a container look like to expedite debug process and can be done using the `--entrypoint` flag as shown below.

```shell

# Override the entrypoint to be a bash shell
docker run -it -v `pwd`:/build --entrypoint /bin/bash simple_test:0.1

# Execute a bash shell within the container
docker exec -it <CONTAINER_ID/CONTAINER_NAME> bash
```

The above command overrides the entrypoint of a Docker container to be `/bin/bash` so we can interact with bash and inspect the internals of the Docker image.


## Build Args

Build args provides us the mechanism to define variables which can be specified at buildtime by a user and are accessible within the Dockerfile.


## [Docker Compose](dockercompose.md)

## Resources

* [Working with docker and registry](https://gist.github.com/kalaspuffar/334f81d11da28df6fa8dbf24910935b0)
* [Creating docker image from scratch and adding to local registry](https://www.youtube.com/watch?v=zqH_G0yNEDw)

* [Dockerfile - Best practices - Docker Con 2019](https://www.youtube.com/watch?v=JofsaZ3H1qM)
* [Complete Docker Course 2020](https://www.youtube.com/watch?v=O-z_vUr53iU&list=PLnFWJCugpwfzyZ7NbYVyajGIVjEsZK5JT)
* [Dockerize any application](https://hackernoon.com/how-to-dockerize-any-application-b60ad00e76da)

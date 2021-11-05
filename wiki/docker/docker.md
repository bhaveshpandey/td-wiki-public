# Docker

## Common commands

Some of the most common commands for querying docker images, containers etc are listed as follows.

```shell

docker image ls
docker container ls
docker ps
docker rm

docker build -t <TAG_NAME> .
docker run <IMAGE_NAME>
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

## Volume Mounting

Often times we require access to persistent data within our docker containers. This can be achieved by mounting volumes with the `-v` flag as shown below.

```shell

docker run -it --rm -v `PATH/TO/MOUNT`:/MOUNT_NAME 'foo-something:0.1'
```

**Where:**

* `PATH/TO/MOUNT` is the directory we want to make accessible to docker container

* `MOUNT_NAME` is the directory it is mapped to within the docker container.


## Resources

* [Complete Docker Course 2020](https://www.youtube.com/watch?v=O-z_vUr53iU&list=PLnFWJCugpwfzyZ7NbYVyajGIVjEsZK5JT)

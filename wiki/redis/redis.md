# Redis

Connecting to a Redis instance using shell. For this, **redis-cli** must be installed.

```shell

redis-cli -h 192.168.1.92 -p 6379
```

Running redis-server in a docker image

```shell

# Run a server
docker run -it --rm --net=host redis:latest
```

We can run a `redis-client` inside a docker container as follows.

```

FROM alpine:latest

RUN apk update --no-cache && apk add --no-cache redis

# This allows users to pass arguments as usual
ENTRYPOINT ["redis-cli"]
```

The above docker image can be run as follows.

`docker run -it --rm --net=host <DOCKER_IMAGE_TAG> -h <HOST_ADDRESS> -p <PORT_NUMBER>`


## Redis Graph

https://oss.redis.com/redisgraph/


## Redis Sentinel

Redis Sentinel provides high availability for Redis. In practical terms this means that using Sentinel you can create a Redis deployment that resists without human intervention certain kinds of failures.

Redis Sentinel also provides other collateral tasks such as monitoring, notifications and acts as a configuration provider for clients.

This is the full list of Sentinel capabilities at a macroscopic level (i.e. the big picture):

* Monitoring - Sentinel constantly checks if your master and replica instances are working as expected.
* Notification - Sentinel can notify the system administrator, or other computer programs, via an API, that something is wrong with one of the monitored Redis instances.
* Automatic failover - If a master is not working as expected, Sentinel can start a failover process where a replica is promoted to master, the other additional replicas are reconfigured to use the new master, and the applications using the Redis server are informed about the new address to use when connecting.
* Configuration provider - Sentinel acts as a source of authority for clients service discovery: clients connect to Sentinels in order to ask for the address of the current Redis master responsible for a given service. If a failover occurs, Sentinels will report the new address.

https://redis.io/topics/sentinel



## Resources

* [Redis Cluster Tutorial](https://oss.redis.com/redisgraph/)

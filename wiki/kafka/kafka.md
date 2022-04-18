# Kafka

## Installing Kafka on Arm 64

* Download the kafka binaries
    `https://dlcdn.apache.org/kafka/3.0.0/kafka_2.13-3.0.0.tgz`

* Untar and rename root dir to kafka
* Cd into kafka directory.
* Create directories as following:
    * mkdir data/{kafka,zookeeper}
* Set the values in following files:
    * config/zookeeper.properties -> dataDir=${ZOOKEEPER_DIR}
    * config/server.properties    -> log.dir=${KAFKA_LOGS_DIR}
    * config/server.properties    -> listeners=PLAINTEXT://192.168.1.25:9092 (IP address of the device)
* Populate the above env vars:
    * ZOOKEEPER_DIR=~/kafka/data/zookeeper
    * KAFKA_LOGS_DIR=~/kafka/data/kafka

Ran the zookeeper server manually as follows:

* KAFKA_LOGS_DIR=/kafka/data/kafka ZOOKEEPER_DIR=/kafka/data/zookeeper bin/zookeeper-server-start.sh config/zookeeper.properties

## Building a custom ARM64 Docker Image

https://docs.ligato.io/en/dev/user-guide/arm64/


Modified `Dockerfile` below:

```Docker

# Kafka and Zookeeper

FROM openjdk:8-jre

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.13
ENV KAFKA_VERSION 3.1.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka, Zookeeper and other needed things
RUN apt-get update && \
    apt-get install -y zookeeper wget supervisor dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    wget -q http://dlcdn.apache.org/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
ADD supervisor/kafka.conf supervisor/zookeeper.conf /etc/supervisor/conf.d/

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
```

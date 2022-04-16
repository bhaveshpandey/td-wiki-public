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

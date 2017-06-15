kafka-cli
============
[![Docker Pulls](https://img.shields.io/docker/pulls/taion809/kafka-cli.svg)](https://hub.docker.com/r/taion809/kafka-cli/)
[![Docker Stars](https://img.shields.io/docker/stars/taion809/kafka-cli.svg)](https://hub.docker.com/r/taion809/kafka-cli/)

### Usage example:
```yaml
version: '3'
services:
    zookeeper:
        image: wurstmeister/zookeeper
        ports:
            - "2181:2181"
    kafka:
        image: wurstmeister/kafka 
        ports:
            - "9092:9092"
        environment:
            KAFKA_CREATE_TOPICS: "test:1:1"
            KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
    producer:
        image: taion809/kafka-cli:0.10.2.0
        command: kafka-console-producer.sh --broker-list kafka:9092 --topic test
        links:
            - kafka
    consumer:
        image: taion809/kafka-cli:0.10.2.0
        command: kafka-console-consumer.sh --bootstrap-server kafka:9092 --topic test --from-beginning
        links:
            - kafka
```

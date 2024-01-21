# learning-apache-kafka
My repo to learn Kafka, setup simple consumers and producers.

This project uses docker to setup Kafka, so ensure that Docker Desktop is installed on your PC. I use a Windows PC so all commands are executed in Windows Powershell. Navigate to the directory where the kafka single node files are located.

Execute the following command from this directory
```
docker-compose -f kafka-single-node.yml up -d
```

> Check if the kafka container are up and running using `docker ps`
> 
> To shutdown and remove the setup, execute this command in the same directory `docker-compose -f kafka-single-node.yml down`

# Topic commands/operations

Logging into the Kafka Container
```
docker exec -it kafka-broker /bin/bash
```
Navigate to the Kafka Scripts directory
```
cd /opt/bitnami/kafka/bin
```

## Creating new Topics
```
./kafka-topics.sh --bootstrap-server localhost:29092 --create --topic kafka.students --partitions 1 --replication-factor 1
```
Here the name of the Kafka topic is kafka.students. Another example:

```
./kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --create \
    --topic kafka.grades \
    --partitions 1 \
    --replication-factor 1
```

## Listing Topics

```
./kafka-topics.sh --bootstrap-server localhost:29092 --list
```

## Getting details about a Topic

```
./kafka-topics.sh --bootstrap-server localhost:29092 --describe
```

## Publishing Messages to Topics

```
./kafka-console-producer.sh --bootstrap-server localhost:29092 --topic kafka.students
```

## Consuming Messages from Topics (or Subscribing)

```
./kafka-console-consumer.sh --bootstrap-server localhost:29092 --topic kafka.students --from-beginning
```

## Deleting Topics

```
./kafka-topics.sh --bootstrap-server localhost:29092 --delete --topic kafka.grades
```

# Example: Students
Creating the kafka.students
```
./kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --create \
    --topic kafka.students \
    --partitions 2 \
    --replication-factor 1
```
Publish to kafka.students
```
./kafka-console-producer.sh \
    --bootstrap-server localhost:29092 \
    --property "parse.key=true" \
    --property "key.separator=:" \
    --topic kafka.usecase.students
```
Consume Message from kafka.students
```
./kafka-console-consumer.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.usecase.students \
    --group usecase-consumer-group \
    --property print.key=true \
    --property key.separator=" = " \
    --from-beginning
```


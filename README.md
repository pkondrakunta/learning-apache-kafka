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


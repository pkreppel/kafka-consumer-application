# Projeto Kafka Consumer
-- Projeto criado seguindo tutorial do site Kafka confluent.
https://kafka-tutorials.confluent.io/creating-first-apache-kafka-consumer-application/kafka.html

#criar containers kafka
docker-compose up -d

## Gradle wrapper
gradle wrapper

## Criar um tópico manualmente
docker-compose exec broker bash
kafka-topics --create --topic input-topic --bootstrap-server broker:9092 --replication-factor 1 --partitions 1

## Compilar e executar com o gradle
./gradlew shadowJar
java -jar build/libs/kafka-consumer-application-standalone-0.0.1.jar configuration/dev.properties

## Criar um console producer
kafka-console-producer --topic input-topic --bootstrap-server broker:9092
Texto teste:
the quick brown fox
jumped over
the lazy dog
Go to Kafka Summit
All streams lead
to Kafka

--> Saída no arquivo consumer-records.out


## Teste com gradle
./gradlew test

## Criar uma imagem
gradle jibDockerBuild --image=io.confluent.developer/kafka-consumer-application-join:0.0.1

## Executar o container
docker run -v $PWD/configuration/prod.properties:/config.properties io.confluent.developer/kafka-consumer-application-join:0.0.1 config.properties

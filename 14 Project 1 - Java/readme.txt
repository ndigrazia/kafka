Kafka - Java

If you use remote Kafka brokers

In case you use Kafka brokers and zookeeper remotely on any of the hosting services like Amazon EC2, Google Cloud or Digitalocean and want to connect to it from your local computer (produce or consume messages) you need to do following:

1. On hosting service firewall allow remote access and open ports 2181 (Zookeeper) and 9092 (Broker)

2. In the configuration file for each broker you need to adjust advertised.listeners and set it either to DNS name or public IP address of the server where broker is hosted.

Examples

advertised.listeners=PLAINTEXT://186.23.16.1:9092
advertised.listeners=PLAINTEXT://ec2-54-123-123-123.compute-1.amazonaws.com:9092

Don't forget to uncomment this line in the configuration file!

If you use only one broker with default configuration file server.properties, do this adjustment in it. If you use multiple brokers in the cluster with multiple configuration files, make this adjustment in each of the custom configuration files



Starting Kafka Cluster

sudo docker-compose -f docker-compose_kafka.yml up -d
sudo docker-compose -f docker-compose_kafka.yml logs
sudo docker-compose -f docker-compose_kafka.yml down



Creating Java Producer

https://kafka.apache.org/documentation/

https://kafka.apache.org/documentation/#api

https://kafka.apache.org/documentation/#producerconfigs

- Messages are sequences of bytes. That's is qhy you need to specify Serializers on Producers & Deserializer on Consumer in order to encode/decode messages key & values.

https://kafka.apache.org/0102/javadoc/org/apache/kafka/common/serialization/Serializer.html

Serializer types: 
ByteArraySerializer, ByteBufferSerializer, BytesSerializer, DoubleSerializer, IntegerSerializer, LongSerializer, StringSerializer


CREATE TOPIC
bin/kafka-topics.sh \
--bootstrap-server localhost:9092 \
--create \
--replication-factor 1 \
--partitions 3 \
--topic numbers

LIST TOPICS
bin/kafka-topics.sh \
--bootstrap-server localhost:9092 \
--list



Explaining most common Producer parameters

https://kafka.apache.org/documentation/#producerconfigs

High importance parameters:

- key.serializer

- value.serializer

Serializer types: 
ByteArraySerializer, ByteBufferSerializer, BytesSerializer, DoubleSerializer, IntegerSerializer, LongSerializer, StringSerializer

- acks
acks=0 (no recommended)

acks=all (recommended)

- bootstrap.servers

- buffer.memory

- compression.type It is recommended selects a compression type.

- retries

- ssl.keystore.<properties>

- batch.size Keep default values is recommended

- client.id 



Creating consumer with autocommitting - PART 1

https://kafka.apache.org/documentation/#consumerapi

-On the consumer you could either enable auto-commit or use manual commit. If a consumer need to do some actions with the messages, for example, you insert them into database or sent to another service, you need to get confirmation of that operation, that you have successfully written messages to the database. Then you could enable manual commiting and send confirmation to brokers only the operation was successfully completed.



Consumer parameters overview

https://kafka.apache.org/documentation/#consumerconfigs

- key.deserializer
- value.deserializer
- bootstrap.servers 
- group.id 
- fetch.min.bytes (default recommended)
- ssl.* 



Consumer with Manual Committing

-On the consumer you could either enable auto-commit or use manual commit. If a consumer need to do some actions with the messages, for example, you insert them into database or sent to another service, you need to get confirmation of that operation, that you have successfully written messages to the database. Then you could enable manual commiting and send confirmation to brokers only the operation was successfully completed.
 


Consumer with Partitions Assignment

TopicPartition partitions[] = {
		new TopicPartition(topic, 2),
		new TopicPartition(topic,4)
};

KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(props);
consumer.assign(Arrays.asList(partitions));



Launching multipile consumers in the same consumer group

Many consumers in the same consumer group will be automatically assigned to diferent partitions. Messages will be received just for one consumer in the group.
 
 

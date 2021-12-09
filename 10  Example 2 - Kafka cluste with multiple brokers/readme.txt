9 Example 2 - Kafka cluste with multiple brokers

Example overview - run multiple brokers

-Every broker must be running in separate port.



Creating separate configuration files for brokers

-You have to have to create several configuration file, one per broker.
- Create diferent copies of server.properties.
- Every broker must have unique port, unique id & unique log folder.
- Create so many copies of server.properties file as broker you have
  Change properties to have unique port, unique id & unique log folder.	
  server0.properties (broker 0) broker.id=0, listeners=PLAINTEXT://:9092, log.dirs=/tmp/kafka-logs-0
  server1.properties (broker 1) broker.id=1, listeners=PLAINTEXT://:9093, log.dirs=/tmp/kafka-logs-1
  server2.properties (broker 2) broker.id=2, listeners=PLAINTEXT://:9094, log.dirs=/tmp/kafka-logs-2


  
Launching three brokers


bin/kafka-server-start.sh config/server0.properties
bin/kafka-server-start.sh config/server1.properties
bin/kafka-server-start.sh config/server2.properties



Getting cluster information and broker details from Zookeeper

Which brokers are able in the cluster?
-bin/zookeeper-shell.sh localhost:2181 ls /brokers/ids


GET INFORMATION FROM ZOOKEEPER ABOUT SPECIFIC BROKER BY ID
bin/zookeeper-shell.sh localhost:2181 get /brokers/ids/0



Creating multiple-partition topic in the Kafka cluster

bin/kafka-topics.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--create \
--replication-factor 1 \
--partitions 5 \
--topic cars

NOTE: if you specify one server, then if it is unavailable you will not be able to create a topic. The operation will fail.



Looking at logs folders of every broker



Producing and consuming messages in the cluster

This produces messages in all available brokers:

bin/kafka-console-producer.sh \
--broker-list localhost:9092,localhost:9093,localhost:9094 \
--topic cars

Recieve all messages from all partitions:

bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--topic cars


Details about topic in the cluster

LIST TOPICS
bin/kafka-topics.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--list

TOPIC DETAILS
bin/kafka-topics.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--describe \
--topic cars



Simulating broker failure in the cluster

START CONSOLE CONSUMER AND READ MESSAGES FROM BEGINNING
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--topic cars   \
--from-beginning

Stop one broker. For example Broker 2.

bin/zookeeper-shell.sh localhost:2181 ls /brokers/ids


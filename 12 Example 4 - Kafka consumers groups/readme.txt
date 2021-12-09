11 Example 4 - Kafka consumers groups

Example with consumer groups overview

Single broker in cluster 
Consumers in the consumer groups

START ZOOKEEPER
bin/zookeeper-server-start.sh config/zookeeper.properties

START KAFKA BROKER
bin/kafka-server-start.sh config/server.properties



Exploring default consumer groups

CREATE TOPIC
bin/kafka-topics.sh \
--bootstrap-server localhost:9092 \
--create \
--replication-factor 1 \
--partitions 5 \
--topic numbers

START CONSOLE PRODUCER
bin/kafka-console-producer.sh \
--broker-list localhost:9092 \
--topic numbers

START CONSOLE CONSUMER
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--topic numbers

LIST CONSUMER GROUPS
bin/kafka-consumer-groups.sh \
--bootstrap-server localhost:9092 \
--list

-Every consumers that we have started, different consumer group will be created. Goals of consumer group is reducing of load consumers.
 A single consumer may not be able to consume all produced message at high rate. That's why we created consumer group to share comsuption of message from same topic.
 Every consumer will get part of the messages in aspecific topic.
 Purpose of consumer group: To reduce of loading consumers.	
 Always a consumer below to specific goup. If you don't specify a gruop, this gorup will be created automtically.
 
 CONSUMER GROUP DETAILS
	bin/kafka-consumer-groups.sh \
	--bootstrap-server localhost:9092 \
	--group nums \
	--describe

 
 
Starting consumer in the custom consumer group

START CONSOLE CONSUMER WITH SPECIFIC CONSUMER GROUP
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--topic numbers \
--group nums \
--from-beginning

LIST CONSUMER GROUPS
bin/kafka-consumer-groups.sh \
--bootstrap-server localhost:9092 \
--list

CONSUMER GROUP DETAILS
bin/kafka-consumer-groups.sh \
--bootstrap-server localhost:9092 \
--group nums \
--describe 

LAG will be non-zero if Consumer  has not yet consumed  all messages in the partition. (CURRENT-OFFSET < LONG-END-OFFSET). This means producers produces messages faster than consume is able to consume.



Starting second consumer in the same consumer group
 

START CONSOLE CONSUMER WITH SPECIFIC CONSUMER GROUP
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--topic numbers \
--group nums \
--from-beginning


START CONSOLE CONSUMER WITH SPECIFIC CONSUMER GROUP
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--topic numbers \
--group nums \
--from-beginning

CONSUMER GROUP DETAILS
bin/kafka-consumer-groups.sh \
--bootstrap-server localhost:9092 \
--group nums \
--describe 

NOTE: Each consumers will be assigned to diferent partitions.
In total 5 partitions, 3 partitions were assigned to first consumer. Remained 3 partitions were assigned to second consumer. 
Each message is consumed once only by single consumer int the group.



Idle consumers in the group

What will happen if qty of consumer is larger than qty of partitions in topic?
Some of the consumers will be idle & will not recieve any messages

if there are 3 partitions witn 100 consumers in the group, 3 will be assigned to the partitions and 97 will be idle.
 
 


10 Example 3 - Multiple brokers & topic with replication



Launching brokers and creating topic with replication
 
START ZOOKEEPER
bin/zookeeper-server-start.sh config/zookeeper.properties

START KAFKA BROKER
bin/kafka-server-start.sh config/server0.properties
bin/kafka-server-start.sh config/server1.properties
bin/kafka-server-start.sh config/server2.properties

GET INFORMATION FROM ZOOKEEPER ABOUT ACTIVE BROKER IDS
bin/zookeeper-shell.sh localhost:2181 ls /brokers/ids

It is not suggested to go beyond te replication factor three or four. Three is complety enough even for production.

CREATE TOPIC
bin/kafka-topics.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--create \
--replication-factor 3 \
--partitions 7 \
--topic months

Total quantity of partitions in topics will be: 7 (partitions) * 3 (replication factor)  = 21 patitions. So for each partition will be two additional replicas.
Every broker has at least 7 partitions.
 
Only single broker (Leader) in the partition servers producers & consumers.
The remainig brokers (follower) simply synchronize messages with leader. The leader replicate messages to follower brokers.
 
 
 
Observing logs folder and details of the topic 

LIST TOPICS
bin/kafka-topics.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--list

Why __consumer_offset topic is missing?
Because we have not yet consumed any message from cluster.

TOPIC DETAILS
bin/kafka-topics.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--describe \
--topic months



Producing and consuming messages in the topic with replication

START CONSOLE PRODUCER
bin/kafka-console-producer.sh \
--broker-list localhost:9092,localhost:9093,localhost:9094 \
--topic months

START CONSOLE CONSUMER
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--topic months

START CONSOLE CONSUMER AND READ MESSAGES FROM BEGINNING
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--topic months \
--from-beginning

START CONSOLE CONSUMER AND READ MESSAGES FROM SPECIFIC PARTITION
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--topic months \
--partition 6 \
--from-beginning

START CONSOLE CONSUMER AND READ MESSAGES FROM SPECIFIC PARTITION AND SPECIFIC OFFSET
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--topic months \
--partition 3 \
--offset 2



Bringing down 2 brokers in the cluster (total 3 brokers)


Bringing back both brokers






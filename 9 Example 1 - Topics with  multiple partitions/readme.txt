9 Example 1 - Topics with  multiple partitions

Cleaning up existing kafka installation

- remove kafka folder
- remove /tmp/kafka-logs folder
- remove /tmp/zookeeper



Creating topic with multiple partitions

bin/kafka-topics.sh \
--bootstrap-server localhost:9092 \
--create \
--replication-factor 1 \
--partitions 3 \
--topic animals

This has created 3 folder on /tmp/kafka-logs
animals-0
animals-1
animals-2

the message are saved on xxxxxxxxxxxxxxxxxxxx.log file



How messages were spread across different partitions

bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--topic animals \
--from-beginning

-With multiple partitions, customers will read messages from multiple partitions. It will be red messages in around robin fashion. It may read in different order as
the messages were produced by a producer. 
- The messages can spread among partitions.



Reading messages from specific partition

bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--partition 1 \
--topic animals \
--from-beginning

bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--partition 2 \
--topic animals \
--from-beginning



Reading messages from specific offset in specific partition

bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--partition 2 \
--topic animals \
--offset 0

bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--partition 2 \
--topic animals \
--offset 1


Reading details about topic and __consumer_offsets

bin/kafka-topics.sh \
--bootstrap-server localhost:9092 \
--list 

bin/kafka-topics.sh \
--bootstrap-server localhost:9092 \
--describe \
--topic animals 

segment.bytes= max size of log nessages file. Segment is a single file that store log messages.
12 Example 5 - Performance testing



Overview of the performance testing example

Multiple broker in the cluster
Testing kafka producer & consume performance

Starting cluster and launching basic performance test

START ZOOKEEPER
bin/zookeeper-server-start.sh config/zookeeper.properties

START KAFKA BROKER
bin/kafka-server-start.sh config/server0.properties
bin/kafka-server-start.sh config/server1.properties
bin/kafka-server-start.sh config/server2.properties

CREATE TOPIC
bin/kafka-topics.sh \
--bootstrap-server localhost:9092 \
--create \
--replication-factor 3 \
--partitions 100 \
--topic perf

START CONSOLE CONSUMER
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--topic perf

PRODUCER PERFORMANCE TEST
bin/kafka-producer-perf-test.sh \
--topic perf \
--num-records 1000 \ //How many messages produces in total
--throughput 100 \    //How many messages produces per second
--record-size 1000 \  //Size of every massage in byte
--producer-props bootstrap.servers=localhost:9092 // properties - List of key & value pairs key(bootstrap.servers) values (localhost:9092)



Increasing performance test parameters
What about 1000000 records and a throughput 10000 per seconds?

bin/kafka-producer-perf-test.sh \
--topic perf \
--num-records 10000 \ //How many messages produces in total
--throughput 1000 \    //How many messages produces per second
--record-size 1000 \  //Size of every massage in byte
--producer-props bootstrap.servers=localhost:9092 // properties - List of key & value pairs key(bootstrap.servers) values (localhost:9092)

bin/kafka-producer-perf-test.sh \
--topic perf \
--num-records 100000 \ //How many messages produces in total
--throughput 10000 \    //How many messages produces per second
--record-size 1000 \  //Size of every massage in byte
--producer-props bootstrap.servers=localhost:9092 // properties - List of key & value pairs key(bootstrap.servers) values (localhost:9092)

bin/kafka-producer-perf-test.sh \
--topic perf \
--num-records 1000000 \ //How many messages produces in total
--throughput 100000 \    //How many messages produces per second
--record-size 1000 \  //Size of every massage in byte
--producer-props bootstrap.servers=localhost:9092 // properties - List of key & value pairs key(bootstrap.servers) values (localhost:9092)

84894.2 record per seconds were performed, no 100000 record per seconds

 Testing consumer performance
 
	CONSUMER PERFORMANCE TEST
	bin/kafka-consumer-perf-test.sh \
	--broker-list localhost:9092 \
	--topic perf \
	--messages 10000

	CONSUMER PERFORMANCE TEST
	bin/kafka-consumer-perf-test.sh \
	--broker-list localhost:9092 \
	--topic perf \
	--messages 100000

	CONSUMER PERFORMANCE TEST
	bin/kafka-consumer-perf-test.sh \
	--broker-list localhost:9092 \
	--topic perf \
	--messages 1000000
	
	if consumers consumes slowly than producers produces there will be LAG between offset.



Getting non-zero LAG values for consumers

CREATE TOPIC
bin/kafka-topics.sh \
--bootstrap-server localhost:9092 \
--create \
--replication-factor 3 \
--partitions 3 \
--topic perf2

2 consumers:

START CONSOLE CONSUMER WITH SPECIFIC CONSUMER GROUP
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--topic perf2 \
--group perf \
--from-beginning
	
START CONSOLE CONSUMER WITH SPECIFIC CONSUMER GROUP
bin/kafka-console-consumer.sh \
--bootstrap-server localhost:9092 \
--topic perf2 \
--group perf \
--from-beginning


CONSUMER GROUP DETAILS
bin/kafka-consumer-groups.sh \
--bootstrap-server localhost:9092 \
--group perf \
--describe


bin/kafka-producer-perf-test.sh \
--topic perf \
--num-records 1000 \ 
--throughput 10 \    
--record-size 100000 \
--producer-props bootstrap.servers=localhost:9092 

CONSUMER GROUP DETAILS
bin/kafka-consumer-groups.sh \
--bootstrap-server localhost:9092 \
--group perf \
--describe

7 What is kafka & how it works

What is Apache Kafka

-it is a distributed publish-suscribe messaging system.


Broker

-Recieve messages from publishers (producer)
-Store messages and send it to suscribers (consumers)



Broker cluster
-Kafka cluster is a collection of brokers 


Zookeeper
-Maintains list of active brokers
-Manages configuration of the topics and partitions.
-Elects controller


Zookeeper ensemble
-Zookeeper cluster (ensemble)
-Quorum: minimus quantities of servers running in order to form operational cluster. Less that quorum, Zookeeper cluster is considered down and all
kafka's brokers will be also down. 	
-It is recommended to have odd number of servers in Zookeeper cluster like 1,3,5,7, etc and quorum set to (n+1)/2. n is qty of servers.


Multiple Kafka clusters
-Multiple cluster in different cowntry or different continent.
-Each cluster will be separate with your own brokers, producers & consumers. Zookeeper is required in each cluster. You can create many cluster as you need.	
What about data synchronization between different cluster?
Mirroring between cluster.


Default ports of Zookeeper and Broker
- zookeepers default port 2181
- kafka broker default port 9092. Use different ports to start up different zookeepers or brokers on single computer.
  To start up different zookeepers or brokers, you need different configuration file and diferent log folder. In case brokers, you need create diferent message folder.

  
 
Kafka Topic
- Store messages
- Unique name in kafka cluster.  
- each message has a specific number called offset. Is assign when it arrives to broker. Unique across partition in specific topic.
  You are not able to insert a message between another message.
-Broker deletes expired message.



Message structure
-Timestamp (assign by kafka broker or producer), offset	number, key (optional), value (sequence of bytes)
- Messages are immutable.
- Idea is kafka stores messages as small as posible.
- key is optinal. They are created on producers. messages with same key, they will be sent to same partition.



Topics and Partitions

-Every topic may exist on diferent brokers included in a kafka cluster.
Why do we need the same topic on different brokers?
For fault tolerance.
-Who does messages spreads among different brokers?
With partitions. One topic may spread in different partitions. Each one on different brokers.
Goals of Partitions: Write/Read messages to hard drive efficiently. partitions increases performace kafka cluster.



Spreading messages across partitions
-Every patition is simply a separate folder with files.
- The messages on partitions are completely different from another partition. They are different messages.
- Every partition must have unique number across all messages. But of the numbers offset across entire topics sholud not unique.
- Every producer decides which partition to write a message.
- What if one broker will fail and one partition will disappear?
If there aren't message replication, messages will disappear.
We need replication a messages to another brokers.



Partition Leader and Followers (replication)
- If a broker fails, the partition simply disappears.
We need to create replica of partitions. 
Leader patition: it handles partition read/write operations.
Follower partition: it simply gets new messages from leader and write into specific patition.
Producer and consumers communicate only with broker with leader partition when want to read or write message to specific partition.
It broker leader fails, one broker becames leader.
That is how to achieve for tolerance using replication. Leader performace most operations.
- Is recommended  to create 2 replicas. To create full tolerance architecture, you need to  have least multiple brokers.
  Two copies of every message, you need to have 3 brokers. You need to configure a replication factor on a topic. It is configured on a topic level basic.
  In this case replication factor is 3. Replication factor 3 is completely enough and will tolerance shutdown of 2 brokers. Recommend to Production enviroment.


  
Controller and it's responsibilities  
-Who decides which broker will be a leader for a particular partition?
 Who decides where partition are spreaded on brokers? Who decides why patition 0 exists on broker 0, patition 1 exists on broker 1, partition 2 exists on broker 2, so on? why not create patition 0, patition 1, patition 2, ... on broker 0?
 Who decides where to move the partition if a broker fails?
 Who decides elect leader, reassign partitions, create new partition and so on?
 This activities are performed by a kafka broker called Controller. It is elected by zookeepers.
 The overhead for this controller is high. You need to plan resources for you kafka brokers accordingly. If controller fails, zookeepers elects other one.
 
 
How Producers write messages to the topic

- A producer can decides to producer messages on different partitions of specific topic.
- 	Every producer may produce  messages to diferent partitions  of specific topic.
. You can select specific partition with key's message. Same key same partition. if you dont supply a key, the message will be spread in a round robin fashion across all partitions in specific topics.



How Consumers read messages from the topic
- Consumer can read messages from several topics.
- Consumer are able to  consume messages either from all partitions or one partitions or several partitions.
- Consumer are able to  consume messages from beginning.
- Consumer are able to  consume messages from specific offset.
- Consumer are able to  consume aonly new messages on specific partition.
- It is posible to create multiple consumers that will consume messages from the single topic. they below to consumer group. Every may be consumed by one consumer in consumer group.


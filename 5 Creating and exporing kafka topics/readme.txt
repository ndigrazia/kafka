Creating and exporing kafka topics

How to connect to Kafka cluster

You need anything kafka server to connect to kafka cluster


Create new Kafka topic

./bin/kafka-topics.sh  //Create, delete or describe a topic.

./bin/kafka-topics.sh  --create --bootstrap-server localhost:9092 --topic cities


Read details about topic

./bin/kafka-topics.sh --list --zookeeper localhost:2181

./bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic cities


If you use remote Kafka brokers
In case you use Kafka brokers and zookeeper remotely on any of the hosting services like Amazon EC2, Google Cloud or Digitalocean and want to connect to it from your local computer (produce or consume messages) you need to do following:

1. On hosting service firewall allow remote access and open ports 2181 (Zookeeper) and 9092 (Broker)

2. In the configuration file for each broker you need to adjust  advertised.listeners and set it either to DNS name or public IP address of the server where broker is hosted.

Examples

advertised.listeners=PLAINTEXT://186.23.16.1:9092
advertised.listeners=PLAINTEXT://ec2-54-123-123-123.compute-1.amazonaws.com:9092
Don't forget to uncomment this line in the configuration file!

If you use only one broker with default configuration file server.properties, do this adjustment in it. If you use multiple brokers in the cluster with multiple configuration files, make this adjustment in each of the custom configuration files.



Installing Node.js with NPM

https://nodejs.org

node -v
npm -v



Starting up Kafka cluster with 3 brokers

START ZOOKEEPER
bin/zookeeper-server-start.sh config/zookeeper.properties

START KAFKA BROKER
bin/kafka-server-start.sh config/server0.properties
bin/kafka-server-start.sh config/server1.properties
bin/kafka-server-start.sh config/server2.properties

GET INFORMATION FROM ZOOKEEPER ABOUT ACTIVE BROKER IDS
bin/zookeeper-shell.sh localhost:2181 ls /brokers/ids

Docker:
sudo docker-compose -f docker-compose_kafka.yml up -d
sudo docker-compose -f docker-compose_kafka.yml logs
sudo docker-compose -f docker-compose_kafka.yml down



Initializing Node.js project

mkdir kafka
cd kafka
npm init



Final Node.js project files

node producer.js
node consumer.js
 
 
 
Creating basic Node.js producer

https://kafka.js.org/

npm install kafkajs



Producing random animal names

Chance - Random generator helper for JavaScript
	https://www.npmjs.com/package/chance
	https://chancejs.com/usage/node.html
	
npm install chance
	
CREATE TOPIC
bin/kafka-topics.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--create \
--replication-factor 3 \
--partitions 5 \
--topic animals

LIST TOPICS
bin/kafka-topics.sh \
--bootstrap-server localhost:9092,localhost:9093,localhost:9094 \
--list



Creating Node.js consumer

https://kafka.js.org/docs/getting-started	


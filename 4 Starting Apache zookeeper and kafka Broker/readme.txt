Starting Apache zookeper and kafka Broker


Observing contents of the Kafka folder

./bin/ execute files
./config  - default configuration for specific service that can be started using execute files
./logs - lods files



Trying to start Zookeeper & kafka Server

#Installation summary:
	Install java
	Download & install kafka

#Start up Zookeeper (zookeper is mandatory in kafka server. Broker will not be started if zookeeper is unavailable.
./bin/zookeeper-server-start.sh ./config/zookeeper.properties

#Start up kafka ( We can run several kafka brokers)
./bin/kafka-server-start.sh ./config/server.properties #Require config file. Default config is located in config folder.

NOTE:

BrokerId - Identify to the broker. Always must be unique on cluster broker
		 - In server.properties you can config BrokerId
/tmp/kafka-logs - kafka will store messages that will be sent by producers and consumers
  
  
  
Observing logs folder and current kafka server setup

	
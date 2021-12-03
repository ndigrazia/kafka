Installing Apache Kafka on remote Ubuntu Server

Creating remote Ubuntu Virtual Private Server
 
 Remote hosting server:
	https://www.vpsserver.com/ubuntu-vps/
	https://www.digitalocean.com/
 
 Digital Ocean (Remote hosting server)
	Create a new project and a new droplet (basically a server)
	

Installing Apache Kafka on Virtual Private Serve

# Install java
	sudo apt-get update
	sudo apt install openjdk-11-jdk
	java --version

#Download apacha kafka
	sudo apt install curl //if you need
	mkdir downloads
	cd downloads	
	curl https://downloads.apache.org/kafka/3.0.0/kafka_2.13-3.0.0.tgz -o kafka.tgz
	mkdir kafka
	cd  kafka
	tar -xvzf ../kafka.tgz --strip 1
	
	on config folder: server.properties has all properties to start up kafka service.
	on bin folder: scripts files to start up kafka service.
	
	
	
	

Fundamentals	Infrastructure	AZ-900-2day	Microsoft Azure Fundamentals (2 Day)	8	Spanish	6/Dec	7/Dec	2	Americas	(GMT-05:00) Eastern Time (US & Canada)	35074	https://esi.microsoft.com/?delid=35074


AZ-900 Microsoft Azure Fundamentals (2 Day)
Date:Dec 06, 2021 - Dec 07, 2021Time:09:00 AM - 05:00 PM Timezone:(GMT-05:00) Eastern Time (US & Canada)Location:VirtualLanguage:Español (Spanish)Available Seats:0/35Delivery Id:35074
https://esi.microsoft.com?delid=35074
https://esi.microsoft.com/Deliveryonly/?delid=35074


AZ-304 Microsoft Azure Architect Design
Date:Dec 13, 2021 - Dec 16, 2021Time:09:00 AM - 05:00 PM Timezone:(GMT-06:00) Guadalajara, Mexico City, MonterreyLocation:VirtualLanguage:Español (Spanish)Available Seats:36/60Delivery Id:34644
VIRTUAL CLASSROOMCopy Link
https://esi.microsoft.com?delid=34644
https://esi.microsoft.com/Deliveryonly/?delid=34644
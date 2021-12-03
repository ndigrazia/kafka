Apache Kafka Installation Overview

Installing Apache Kafka on the Mac

https://kafka.apache.org/downloads

curl https://dlcdn.apache.org/kafka/3.0.0/kafka_2.13-3.0.0.tgz -o Downloads/kafka.tgz	
cd Downloads
ls -la Downloads


mkdir kafka
cd kafka
tar -xvzf  Downloads/kafka.tgz --strip 1
ls -la

IMPORTANT: We must install java. Kafka was developed in java

java --version



Installing Ubuntu on MacOS using VirtualBox

#Download virtualbox 
https://www.virtualbox.org/wiki/Downloads

#Download ubuntu 
https://ubuntu.com/download/desktop

#Install VirtualBox

#Create VirtualBox machine with 2048 MB, 10 GB size of hard disk.	

#Attach iso image (ubuntu image) to virtual machibe created. 	
	Setting-> Storage
		- on Controller:IDE choose Empty, click on disk icon and select "Choose disk file".
		- select image ubuntu downloaded.
			
#Start virtual machine.

#Install ubuntu on machine machine virtual.
 To get full screen, install "Guest additions CD images". Divices menu-> Insert Guest additions CD images...
	Later, click on VBox_gas_<version number> icon and run. 
		if VBox_gas_<version number> icon isnot installed:
			click Machine menu->ACPI Shutdown. After that, click Setting -> Storage	
				Create a virtual CD:
					Click on blue disk ico and select "optical Drive". After that, click on "Leave Empty". You see a new disk attached.
						Try up install "Guest additions CD images" agains.
						
						
 
	



# Install zookeeper
1. download zookeeper to your windows   
http://zookeeper.apache.org/releases.html#download

2. unzip to path   
e.g. C:\Users\fchen\zookeeper-3.4.14

3. add system environment val   
ZOOKEEPER_HOME   C:\Users\fchen\zookeeper-3.4.14   

append to path   
%ZOOKEEPER_HOME%\bin

4. rename config/zoo_sample.cfg to config/zoo.cfg   

5. update dataDir from /tmp/zookeeper to   
dataDir=C:\\Users\\fchen\\zookeeper-3.4.14\\data

6. start zookeeper   
zkserver

# Install Kafka
1. download kafka to your windows   
https://www.apache.org/dyn/closer.cgi?path=/kafka/2.2.0/kafka_2.11-2.2.0.tgz   

2. unzip to path   
e.g. C:\Users\fchen\kafka_2.11-2.1.1   

3. update config/server.properties   
log.dirs=C:\\Users\\fchen\\kafka_2.11-2.1.1\\kafka-logs

4. start kafka   
.\bin\windows\kafka-server-start.bat .\config\server.properties

5. create topic   
 bin\windows\\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic NCT

list topics   
 bin\windows\kafka-topics.bat --zookeeper localhost:2181 --list

6. produce topic   
 bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic NCT
 
7. consume topic   
 bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic NCT --from-beginning

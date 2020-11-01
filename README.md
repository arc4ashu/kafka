Kafka learning 
------------------
Download the kafka library from apache kafka distributer</br>
https://kafka.apache.org/downloads</br>

</br>
</br>

extract the download folder
go to bin folder
</br>
Make sure you are navigated inside the bin directory.</br>
<b>Start Zookeeper and Kafka Broker </b> </br>
<i>Start up the Zookeeper.</i></br>
./zookeeper-server-start.sh ../config/zookeeper.properties</br>
</br>
</br>
<i>Add the below properties in the server.properties</i></br>
listeners=PLAINTEXT://localhost:9092</br>
auto.create.topics.enable=false</br></br>
Start up the Kafka Broker</br>
./kafka-server-start.sh ../config/server.properties</br>
How to create a topic ?</br>
./kafka-topics.sh --create --topic test-topic -zookeeper localhost:2181 --replication-factor 1 --partitions 4</br>
How to instantiate a Console Producer?</br>
Without Key</br>
./kafka-console-producer.sh --broker-list localhost:9092 --topic test-topic</br>
With Key</br>
./kafka-console-producer.sh --broker-list localhost:9092 --topic test-topic --property "key.separator=-" --property "parse.key=true"</br>
How to instantiate a Console Consumer?</br>
Without Key</br>
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test-topic --from-beginning</br>
With Key</br>
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test-topic --from-beginning -property "key.separator= - " --property "print.key=true"</br>
With Consumer Group</br>
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test-topic --group <group-name></br>
Windows</br>
Setting Up Multiple Kafka Brokers</br>
The first step is to add a new server.properties.</br>

We need to modify three properties to start up a multi broker set up.</br>

broker.id=<unique-broker-d></br>
listeners=PLAINTEXT://localhost:<unique-port></br>
log.dirs=/tmp/<unique-kafka-folder></br>
auto.create.topics.enable=false</br>
Example config will be like below.</br>
broker.id=1</br>
listeners=PLAINTEXT://localhost:9093</br>
log.dirs=/tmp/kafka-logs-1</br>
auto.create.topics.enable=false</br>
Starting up the new Broker</br>
Provide the new server.properties thats added.</br>
./kafka-server-start.sh ../config/server-1.properties</br>
./kafka-server-start.sh ../config/server-2.properties</br>
Advanced Kafka CLI operations:</br>
Mac</br>
List the topics in a cluster</br>
./kafka-topics.sh --zookeeper localhost:2181 --list</br>
Describe topic</br>
The below command can be used to describe all the topics.</br>
./kafka-topics.sh --zookeeper localhost:2181 --describe</br>
The below command can be used to describe a specific topic.</br>
./kafka-topics.sh --zookeeper localhost:2181 --describe --topic <topic-name></br>
Alter the min insync replica</br>
./kafka-topics.sh --alter --zookeeper localhost:2181 --topic library-events --config min.insync.replicas=2</br>
Delete a topic</br>
./kafka-topics.sh --zookeeper localhost:2181 --delete --topic test-topic</br>
How to view consumer groups</br>
./kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list</br>
Consumer Groups and their Offset</br>
./kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group console-consumer-27773</br>
Viewing the Commit Log</br>
./kafka-run-class.sh kafka.tools.DumpLogSegments --deep-iteration --files /tmp/kafka-logs/test-topic-0/00000000000000000000.log</br>
Setting the Minimum Insync Replica</br>
./kafka-configs.sh --alter --zookeeper localhost:2181 --entity-type topics --entity-name test-topic --add-config min.insync.replicas=2</br>



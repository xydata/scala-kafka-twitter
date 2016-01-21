
######This Project is a folk of mkrcah/scala-kafka-twitter######

### Demonstration project to monitor Twitter stream to identify & act on unexpected increases in tweet volume 

This is WIP.

Current infrastructure:
- Tweets are serialized to Avro (without code generation) and sent to Kafka
- A Kafka consumer picks up serialized Tweets and prints them to stdout

![image](https://docs.google.com/drawings/d/1jVxh473mabBTm5tDIDd7dRRDgrNGorXefEp6ZDdyIyc/pub?w=960&h=720)

### How to run

1. Get Twitter credentials and fill them in `reference.conf`.

2. Start Kafka [(instructions)](http://kafka.apache.org/documentation.html#introduction) in single-node mode on localhost

3. Start Kafka producer
```
./gradlew produce 
```
This will start to read recent tweets, encode them to Avro and send to the Kafka cluster in binary format (`Array[Byte]`). 

4. Start Kafka consumer
```
 ./gradlew consume
```
This will run Spark streaming connected to the Kafka cluster. In 5-second intervals 
the program reads Avro tweets from Kafka, deserializes the tweet texts to strings 
and print 10 most frequent words
 


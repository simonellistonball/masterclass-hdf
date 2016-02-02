# Lab 4: External Sources

Let's looks at some external data sources

1. Create a ListenHTTP processor
  1. Set the listening port to 9091
  1. Set the base path to "hello"

This is a web listener

1. Feed this into a PutFile processor.

Use curl to send data to this:
curl -d"data" -X POST http://hostname:9091/hello

You will see this in your flow.

Let's also look at the syslog listener

1. Create a ListenSyslog processor.
  1. Note the batching options here.
1. Push this to a PutFile.

A common pattern is the List, Fetch patter.

1. Create a ListSFTP processor
1. Create a FetchSFTP processor
1. Connect them up

Investigate the many ingest options!

#Egress options
Go back to your HDP cluster, with the PutHDFS piece. Let's push the individual lines into Kafka

1. Add a PutKafka processor.
1. Configure the broker list property to point to localhost:6667, and the topic 'test'

1. ssh into the hdp cluster and create the kafka topic (/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --topic test --partitions 1 --replication-factor 1 --zookeeper localhost:2181)
1. Run the PutKafka processor

Test this by pushing files into your flow input folder. Lines appear one by one in Kafka, and as a block in HDFS.

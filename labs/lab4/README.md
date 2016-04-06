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
  1. NiFi is running as a non-privileged user, so you will not be able to use the default port (514) try 1514 instead, and point syslog to this instead.
1. Push this to a PutFile
  1. Warning: By default, each new log record (row) will write to a new file
1. (optional) Update & restart rsyslog to forward all logs to NiFi
  1. `echo '*.* @localhost:1514' | sudo tee -a /etc/rsyslog.conf ; sudo service rsyslog restart`

A common pattern is the List, Fetch patter.

1. Create a ListSFTP processor
1. Create a FetchSFTP processor
1. Connect them up

Investigate the many ingest options!

#Egress options
Go back to your HDP cluster, with the PutHDFS piece. Let's push the individual lines into Kafka

1. Add a PutKafka processor.
1. Configure the broker list property to point to ip_address:6667, and the topic 'test'

1. ssh into the hdp cluster and create the kafka topic (/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --topic test --partitions 1 --replication-factor 1 --zookeeper localhost:2181)
1. Run the PutKafka processor

Test this by pushing files into your flow input folder. Lines appear one by one in Kafka, and as a block in HDFS.

To see the files in Kafka,
   run /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test
on your kafka box.

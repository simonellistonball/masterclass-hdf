# Lab 4: External Sources

Let's looks at some external data sourcse

1. Create a ListenHTTP processor
  1. Set the listening port to 8188
  1. Set the base path to /hello

This is a web listener

1. Feed this into a PutFile processor.

Use curl to send data to this:
curl -d"data" -X POST http://hostname:8188/hello

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

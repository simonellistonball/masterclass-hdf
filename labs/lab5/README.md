# Lab 4: Remote Clusters

1. On your HDP cluster, setup an input port in the root canvas
1. Wire this up to the HDFS Ingest group.

Now setup the instance in the shell.

1. Edit nifi.properties in /opt/nifi-1.1.1.0-12/conf/
1. Set nifi.remote.input.socket.port=9091
1. Set nifi.remote.input.secure=false
1. Restart the nifi service (/opt/nifi-1.1.1.0-12/bin/nifi.sh restart, or via Ambari)

1. On your single nifi node, setup a file collection flow, or use the one you already have.
1. Create a remote process group.
1. Enter the URL of your remote NiFi cluster

You can then Enable Transmission on this remote process group. It behaves just like a regular process group, and you can wire up a Flow to the input port. 

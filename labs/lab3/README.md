# Lab 3: Process Groups and Organisation

So far we've been putting all the flows into the root canvas. This is fine for simple flows, but sometimes you need a bit of organisation.

First Let's create a simple flow.

1. Create a GetFile processor
1. Create a SplitText processor
  1. configure it with a line count of 1 in the properties


Now we want to write this to HDFS. That is often repeated and takes a few steps, lets group them.

1. Drag a processor group from the toolbar.
1. Give it a name
1. Double click into it, you will get a new canvas.

Now in the new blank canvas:

1. Drag an input port onto the canvas, and call it "Lines"
1. Add a MergeContent processor and configure it with BinPacking
  1. Set the min size to a few Lines
  1. Set the max age to a few minutes
  1. Set max size to 128MB
1. Add an UpdateAttribute to change the filename
1. Add CompressContent, use bzip2
1. Add PutHdfs
  1. Configure the properties to point to the hadoop config files (/etc/hadoop/conf/core-site.xml,/etc/hadoop/conf/hdfs-site.xml)
  1. Set a directory (and make sure it exists of HDFS and the nifi user has permissions, /tmp is a good place for now)

1. Add and output port.

1. Now connect up all these pieces with the relevant relations.
1. Set the MergeContent schedule to run every 5 minutes.

You can now escape up to the root canvas with the bread crumb trail at the top of the screen.

1. Now hook the output of the flow on the root canvas to the input port in the ProcessGroup.

Note that process groups can be paramaterised with the attribute expression language and attributes being fed in, and can have as many inputs and outputs as your flow requires.

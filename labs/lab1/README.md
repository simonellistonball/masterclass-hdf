#Lab 1: Building a basic flow

Starting with a blank NiFi canvas.

1. Drag the processor icon onto the canvas.
1. Explore the available processors
1. Select the GetFile Processor and add it
1. Configure the GetFile Processor
  1. Right-click on the new processor
  1. Select "Configure"
  1. The tabbed dialog should show settings, give the processor a name
  1. Select the properties tab
  1. Input "/tmp/input" (make sure you create this directory on your NiFi box, and that it is owned by the nifi user - chown -R nifi:nifi /tmp/input)
1. Now add an UpdateAttribute processor
  1. Configure it with a new dynamic property
    1. In the properties tab, press the plus sign in the top right of the dialog
    1. Call the property "filename" and set the value to something meaningful
    1. Add a property called "mime.type" and set this to "application/gzip"
1. Connect the two processors
  1. Hover over the GetFile processor, until the begin connection icon appears
  1. Drag this onto the UpdateAttribute processor
  1. This brings up the connection configuration dialog
    1. For now just leave this on defaults.
1. Add a CompressContent processor and look at its properties, the defaults should work fine here.
1. On settings, make sure you set "Autoterminate relationships" on for failure
configure it
1. Now connect up the output of our UpdateAttributes processor to the new CompressContent
1. Add a PutFile processor
1. Configure the destination location in the PutFile processor properties. Note the conflict resolution strategy, and set this to replace. (nifi will create this directory for you)
1. Set both success and failure relationships to auto-terminate in the settings tab

1. Setup the connection between the CompressContent processor and the PutFile processor (only for the success relation!)

Now you have you first complete flow, press play at the top of the screen (make sure you don't have a processor selected)

If you copy a file (for example /var/log/ambari-agent/ambari-agent.log) to the input folder you chose, NiFi will pick it up a compress it into the output directory you chose. Take a minute to verify this behaviour.

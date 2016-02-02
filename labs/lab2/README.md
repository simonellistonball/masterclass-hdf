#Lab 2: Adding to the flow

Starting with a the existing flow from Lab 1.

We are going to add a new processor to this flow. Note that this can be done while the flow is running.

First add the new processor, we will use a GetHTTP processor, this fetches the contents of a web page.

1. Drag the processor icon onto the Canvas
1. Select the GetHTTP processor
1. Configure the new processors:
  1. Here we want to be very careful about scheduling
  1. Select scheduling
  1. Set the run schedule to "1 min" (we can also use other times and units of time)
  1. In properties, pick the url of your favourite website (keep it safe for work!)
  1. Set a filename, this is what the filename attribute will be set to.
1. Now lets hook this up to our existing flow:
1. Connect this into the UpdateAttribute processor we used before.
1. Now right-click your new processor and "Start" it.

You should now see activity in the processor, check the numbers of tasks and the bytes in an out in the processor block to ensure you are getting data.

Copies of your site will be compressed and stored into the output folder we previously set. Check this out to see that the html is arriving safely.

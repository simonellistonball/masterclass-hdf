# Lab 6: Routing on Attributes and Priorities

Prioritisation is a key element of NiFi. Let's set up some queue priorities.

Starting with our SplitText based example, let's extract some content, and route things differently.

We are only interested in seeing security events in Kafka, we also want them processed faster.

1. After SplitLines, add a new processor group
1. Use ExtractText with a new dynamic property called security, set the match pattern to "(.*auth.*)"
1. Insert an UpdateAttribute processor, this will get a custom attribute calls "priority" and set it to "10"
1. Add a dynamic property called failed, and set this to "${security:contains("failed")}"
1. Add a RouteOnAttribute processor, and pick out two routes with dynamic properties, for example:
  1. "certificate issue", ${security:contains('certificate')}
  1. "login failed", ${security:contains('login')}

1. Route each of these to a different UpdateAttribute processor, and use them to set the priority attribute to a 5 and 1 respectively.

1. Create funnel and route both these processors into the funnel.

1. Now create a route to your remote cluster from the funnel, and set the prioritisers to PriorityAttributePrioritiser

Let's also look at better names for our HDFS files, so in our HDFS group, use the UpdateAttribute to set a filename. Change the filename property to "${now():format("yyyyMMddhhmm")}"

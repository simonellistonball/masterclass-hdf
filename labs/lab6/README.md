# Lab 6: Routing on Attributes and Priorities

Prioritisation is a key element of NiFi. Let's set up some queue priorities.

Starting with our SplitText based example, let's extract some content, and route things differently.

We are only interested in seeing security events in Kafka, we also want them processed faster.

1. After SplitLines, add a new processor group
1. Use ExtractText with a new dynamic property called security, set the match pattern to "(.*auth.*)"
1. Insert an UpdateAttribute processor, this will get a custom attribute calls "security" and set it to "1"
1. Add a dynamic property called priority, and set this to "${security:contains("failed")}"
1. Route the matched relation to the Kafka queue, but set the prioritisers to PriorityAttributePrioritiser
1. Route the unmatched back to the HDFS queue

At the same time, lets give our files a better name

For the UpdateAttribute settings filename, change the filename property to "${now():format("yyyyMMddhhmm")}"

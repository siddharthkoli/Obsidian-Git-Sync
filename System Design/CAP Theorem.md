In a distributed computer system, you can only support two of the following guarantees:

- **Consistency** - Every read receives the most recent write or an error.
- **Availability** - Every request receives a response, without guarantee that it contains the most recent version of the information. Here, the system is guaranteed to return a response (will not throw error), but may return stale data.
- **Partition Tolerance** - A network partition occurs when communication between nodes in a distributed system is disrupted, resulting in the formation of isolated groups of nodes. Each group (partition) operates independently due to the lack of communication with nodes in other partitions. A distributed system that is partition-tolerant can continue to function and provide responses even in the presence of network partitions.

Network failures _happen to your system_ and you don't get to choose when they occur.
*network partitions can and will occur in a distributed system.
Given that networks aren't completely reliable, you must tolerate partitions in a distributed system, period.
Networks aren't reliable, so you'll need to support partition tolerance. You'll need to make a software tradeoff between consistency and availability.


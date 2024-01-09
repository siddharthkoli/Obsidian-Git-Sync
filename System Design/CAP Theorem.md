In a distributed computer system, you can only support two of the following guarantees:

- **Consistency** - Every read receives the most recent write or an error.
- **Availability** - Every request receives a response, without guarantee that it contains the most recent version of the information. Here, the system is guaranteed to return a response (will not throw error), but may return stale data.
- **Partition Tolerance** - A network partition occurs when communication between nodes in a distributed system is disrupted, resulting in the formation of isolated groups of nodes. Each group (partition) operates independently due to the lack of communication with nodes in other partitions. A distributed system that is partition-tolerant can continue to function and provide responses even in the presence of network partitions.

Network failures _happen to your system_ and you don't get to choose when they occur.
Network partitions ****can and will occur**** in a distributed system.
Networks aren't reliable, so you'll need to support partition tolerance. You'll need to make a software tradeoff between consistency and availability.

Given that networks aren't completely reliable, you must tolerate partitions in a distributed system, period. This means we are left with two options: Consistency and Availability.

- **CP** - Consistency/Partition Tolerance - Wait for a response from the partitioned node which could result in a timeout error. The system can also choose to return an error, depending on the scenario you desire. Choose Consistency over Availability when your business requirements dictate atomic reads and writes.
		Basically - Give the most latest write. If not throw error or wait for system to become consistent.
- **AP** - Availability/Partition Tolerance - Return the most recent version of the data you have, which could be stale. This system state will also accept writes that can be processed later when the partition is resolved. Choose Availability over Consistency when your business requirements allow for some flexibility around when the data in the system synchronizes.
		 Basically - Return response at any cost. Response could be stale.



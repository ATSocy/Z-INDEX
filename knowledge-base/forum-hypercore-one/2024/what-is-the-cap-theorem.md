Thread: what-is-the-cap-theorem
0x3639 | 2023-12-21 11:32:45 UTC | #1

Good (and simple) video that describes the CAP Theorem.  

https://youtu.be/BHqjEjzAicA?si=UmUgetZKcuvBEIqU

## Background

The theorem states that it is impossible for a distributed data store to simultaneously provide more than two out of the following three guarantees:

1. **Consistency**: Every read receives the most recent write or an error. This means that all nodes see the same data at the same time.
2. **Availability**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write. This means the system is always up and running, and every request gets a response, but the response might not be the most up-to-date.
3. **Partition Tolerance**: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes. In other words, the system can continue to operate even if there is a "partition" (a communication breakdown) between two nodes caused by network failure.

According to the CAP theorem, a distributed system can only provide two of these three guarantees at the same time, not all three. For example, if a system prioritizes consistency and partition tolerance, it might not be able to maintain availability, leading to system downtime during network partitions.

This theorem is a central concept in distributed computing and has significant implications for the design of distributed databases, distributed file systems, and other similar technologies. It helps system designers to understand the trade-offs between different system properties and to make informed decisions about their architecture.

[Source: ChatGPT]

-------------------------


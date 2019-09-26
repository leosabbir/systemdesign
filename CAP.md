# CAP Theorem

## Definition of Consistency, Availability and Partition Tolerance
- Consistency: Every read receives the most recent write or an Error
- Availability: Every request receives a non-error response, without the guarantee that it contains the most recent write.
- Partition Tolerance: The system continues to operate despite an arbitrary number of messages being dropped or delayed by the network between nodes.


## Misconception & Theorem
> CAP is frequently misunderstood as if one has to choose to **abandon one of the three guarantees** at all times.

> In fact, the choice is really between **Consistency** and **Availability** ONLY when a **Network Partition** or **Failure** happens.

> At **All** other times, **No Trade Off** has to be made - that is, in the absence of network failure, when the distributed system is running normally – both availability and consistency can be satisfied.

## Implication
No distributed system is safe from network failures, thus network partitioning generally has to be tolerated. In the presence of a partition, one is then left with one of the two options: Consistency or Availability.
1. When choosing consistency over availability, the system will return an error or a time-out if particular information cannot be guaranteed to be up to date due to network partitioning.
2. when choosing availability over consistency, the system will always process the query and try to return the most recent available version of the information, even if it cannot be guarantee it is up to date due to network partitioning.

## Conclusion
In summary, when a network partition or failure happens, we have to decide either to:
1. Cancel the operation and thus decrease the availability but ensure Consistency.
2. Proceed with the operation and thus provide Availability but risk Inconsitency.


## Examples:
- RDBMS designed with tranditional ACID guarantees choose consistency over availability.
- Systems designed around BASE philosopy, common in the NoSQL movement chhose availability over consistency.
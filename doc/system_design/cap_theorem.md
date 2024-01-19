# CAP Theorem

The CAP theorem is a `concept in distributed systems that states a system can only guarantee two out of the following three properties`: Consistency, Availability, and Partition Tolerance.

!!! note "Consistency"
    `Every read receives the most recent write or an error`. In other words, `all nodes see the same data at the same time`. This means that `any data written to the system will be immediately visible` to all subsequent reads.

!!! note "Availability"
    `Every request receives a non-error response, without the guarantee that it contains the most recent write`. This means that even if the system cannot find the most current data, it still responds to requests instead of failing.

!!! note "Partition Tolerance"
    `The system continues to operate despite arbitrary partitioning due to network failures`. This means that the `system remains operational even if some of the nodes are unable to communicate with others`.

The CAP theorem states that in the event of a `network partition`, a system can `only guarantee two of these three properties`. For example, if a system is designed to prioritize availability and partition tolerance, `it may serve stale data to ensure that every request receives a response`, even if that data is not the most recent. On the other hand, if a system is designed to prioritize consistency and partition tolerance, `it may refuse to respond to requests if it cannot verify the data's consistency` across all nodes.

It's important to note that the CAP theorem `does not imply that it's impossible to build a system that satisfies all three properties`. Rather, it `states that in the face of a network partition, a system can only guarantee two out of the three properties`. Therefore, when designing a `distributed system`, developers must make a conscious decision about which two properties they want to prioritize.

## References

1. [What is the CAP theorem?](https://www.ibm.com/topics/cap-theorem)
1. [System design fundamentals: What is the CAP theorem?](https://www.educative.io/blog/what-is-cap-theorem)

# Capacity Plan

!!! tip
    1. KB → MB = KB/10^3
    1. MB → GB = MB/10^3
    1. GB → TB = GB/10^3
    1. MB → TB = MB/10^6

Capacity planning is a critical aspect of system design. `It involves estimating the maximum load that a system can handle, including the number of users, transactions, or data that the system can process without performance degradation`. Effective capacity planning can help `avoid bottlenecks`, `ensure system scalability`, and prevent `costly resource over-allocation`. Capacity planning is an `iterative process`. As the system grows and evolves, the `capacity requirements may change`, and the capacity planning should be updated accordingly.

## Key Steps

Here are some key steps involved in capacity planning:

!!! note "Estimate Options"
    `Start by estimating the scope of the system`. Your initial measure for quantifying capacity is usually an `assumed throughput`, `inferred from a similar feature or another number such as daily active users`. Then, come up with a ballpark `estimate of how much a request costs in bytes`. For `object storage`, consider factors like versioning and the average size of different media files. Once you know how much each record costs, think of `bandwidth per operation`.

!!! note "Peak QPS"
    `Calculating peak Query Per Second (QPS)` is important as it often dictates the capacity requirement of the design. `Peak QPS refers to the highest rate at which a system will be expected to handle queries`, often occurring during times of high usage or traffic spikes. This can be `determined through historical data analysis`, predicting event-driven peaks, or time-driven peaks.

!!! note "Understanding Request Sizes"
    Assessing request sizes is `crucial for determining bandwidth and storage requirements`. Depending on the system's functionality and the nature of data it handles, you can make informed assumptions about the size of different types of requests.

!!! note "Throughput Calculation"
    Throughput is an important metric for capacity planning. `It represents the number of requests that can be handled by the system in a given time frame`. Throughput can be `calculated based on the system's requirements or inferred from relevant metrics like daily active users`.

!!! note "Estimating Server Requirement"
    With the estimated throughput and response time, you can `estimate the number of servers needed to run the application`. This calculation takes into account the average response time per request and the number of workers each server can handle.

!!! note "Bandwidth & Data in Transit"
    Understanding `each record’s cost` is fundamental. You need to `consider the bandwidth per operation in both directions` - client to server (ingress) and server to client (egress).

!!! note "Be Prepared to Operate"
    Much of the truly challenging work for capacity planning is in `operating capacity`. Sometimes, `assumptions made during the design stage may not hold true in practice`. Therefore, c`ontinuous planning and monitoring is extremely important`. Writing some of the assumptions made at the design stage in the form of alerts can help detect misconceptions. Using concepts of threat modeling can help understand which safeguards are missing, what happens if a certain characteristic changes, or if a non-functional requirement changes.

!!! note "Rounding and Approximation"
    It is difficult to perform complicated math operations during the interview. `There is no need to spend valuable time to solve complicated math problems. Precision is not expected`. Use round numbers and approximation to your advantage.

## Calculate Request By Second(RPS)

Calculating the number of requests per second (RPS) is a critical part of system design and performance estimation. `It helps determine how many requests your system can handle in a single second`.

Considering:

1. 1Mi DAU (Daily Active Users)
1. 5 request by user on daily average
1. 100.000 seconds by day or 10^5

!!! tip "Seconds by Day Calculation"
    Normaly, one day has 86.500 seconds. However, as mentioned in Round and Approximation note in [Key Steps](#key-steps) is normal to round to facilitate the calculation. So there is no problem to say that one day has 100.000 seconds or 10^5.

Calculating:

1. 1.000.000 * 5 = 5.000.000 `requests by day`
1. 5.000.000 / 100.000 = 50 `requests by second (RPS)`

OR

1. 5 \* 10^6 / 10^5 = 5 \* 10^6-5
1. 5 \* 10^1 = 50 RPS

!!! example "Write and Read"
    Considering:

    1. Read VS Write = 9:1

    Calculate:

    1. Writes = 50rps * 0.1 = 5rps
    1. Read = 50 * 0.9 = 45rps

!!! example "Purchases by Seconds"
    Considering:

    1. 5% of users buy something

    Calculate:

    1. `5% of 1Mi = 50.000 per day` or `5% of 10^6 = 5*10^4`
    1. 5\*10^4 / 10^5 (secods by day) = 5\*10(4-5) = 5\10^-1
    1. `0.5 purchases by seconds`

## Calculate Peak Query Per Second (QPS)

## Bandwidth

`Bandwidth refers to the maximum rate of data transfer across a given path`. It's typically measured in bits per second (bps), kilobits per second (Kbps), megabits per second (Mbps), gigabits per second (Gbps), or terabits per second (Tbps). Bandwidth is a crucial factor in system design as it `directly influences the system's performance and scalability`.

!!! note "Steps to Calculate"
    1. `Identify the Data Transfer Rate`: This is the `speed at which data is transferred over the network`. It's usually provided by the network service provider and is typically measured in bits per second (bps). For example, a 1 Gbps network has a data transfer rate of 1,000,000,000 bits per second.
    1. `Calculate the Number of Users`: This is the number of `users that will be using the network simultaneously`. For example, if you have a network with a data transfer rate of 1 Gbps and you have 100 users, `each user will have a bandwidth of 10 Mbps` (1 Gbps / 100 users)
    1. `Calculate the Bandwidth Usage Per User`: This is the `amount of data that each user will be transferring over the network`. For example, if each user is transferring 10 MB of data per second, the bandwidth usage per user will be 10 Mbps.
    1. `Calculate the Total Bandwidth Usage`: This is the `total amount of data that will be transferred over the network`. It's `calculated by multiplying the bandwidth usage per user by the number of users`. For example, if each user is using 10 Mbps and there are 100 users, the total bandwidth usage will be 1 Gbps.

!!! example "First Example"
    Suppose you have a network with a `data transfer rate of 1 Gbps` (1,000,000,000 bits per second). You have `100 users`, each of whom will be `transferring 10 MB of data per second`. The `total bandwidth usage would be 1 Gbps` (10 Mbps \* 100 users).

!!! example "Second Example"
    Considering:

    1. 50 request per second (rps)
    1. Each request size is 50Kb

    Calculate:

    1. 50rps * 50kb = 2500Kb/s
    or
    1. 2500Kb/s / 1000 = 2.5Mb/s
    or
    1. 2.5*10^3 / 10^3 = 2.5*10^(3-3) = 2.5Mb/s

## References

1. [System Design — Capacity Estimation](https://medium.com/@cribeirorodrigues/system-design-capacity-estimation-a34309f88914)
1. [System Design: Capacity Planning basics](https://dballona.com/system-design-capacity-planning-basics)
1. [Capacity Planning](https://blog.bytebytego.com/p/capacity-planning)
1. [Back-of-the-envelope Estimation](https://bytebytego.com/courses/system-design-interview/back-of-the-envelope-estimation)
1. [How to calculate network bandwidth requirements](https://www.techtarget.com/searchnetworking/tip/How-to-calculate-network-bandwidth-requirements)

<!-- Commonly asked back-of-the-envelope estimations: QPS, peak QPS, storage, cache, number of servers, etc. You can practice these calculations when preparing for an interview. Practice makes perfect. -->
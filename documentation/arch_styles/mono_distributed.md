# Monolithic vs Distributed Architectures

There are `two primary categories`: monolithic and distributed architectures. These categories serve as a foundational distinction, even though it's important to note that `no classification is perfect`. `Distributed architectures, in particular, introduce a unique set of challenges that set them apart from monolithic architectures`. This classification offers a valuable way to differentiate between various architectural styles.

## Monolithic List

1. Layered Architecture
1. Pipeline Architecture
1. Microkernel Architecture

## Distributed List

1. Service-based Architecture
1. Event-driven Architecture
1. Space-based Architecture
1. Service-oriented Architecture
1. Microservices Architecture

## Fallacies of Distributed Computing

Distributed architectures `can be more` powerful in terms of performance, scalability, and availability than monolithic architecture styles, `but they come with trade-offs`. `Some common misconceptions, can lead to false assumptions in distributed systems`. Understanding these misconceptions is crucial in designing distributed architectures.

### The Network Is Reliable

`People often assume that networks are reliable, but they're not`. Even though networks have improved, they can still be unreliable. `This is critical in distributed architectures because they heavily depend on network communication`. Measures like timeouts and circuit breakers are used to manage this unpredictability, especially in systems like microservices. `The more a system relies on the network, the less reliable it can be`. Latency in any distributed architecture is not zero, yet most architects ignore this fallacy, insisting that they have fast networks.

### Latency Is Zero

`Local calls between components are faster than remote ones using protocols like REST, messaging, or RPC`. `Knowing the average round-trip latency for remote calls is crucial in distributed architectures`, especially microservices.

??? tip "Calculating Latency"
    If the average latency is 100 milliseconds, chaining 10 service calls adds 1,000 milliseconds to a request. `However, it's not just the average latency that matters; the 95th to 99th percentile can significantly impact performance`. So, understanding these latencies is vital for architecting distributed systems.

### Bandwidth Is Infinite

### The Network Is Secure

### The Topology Never Changes

### There Is Only One Administrator

### Transport Cost Is Zero

### The Network Is Homogeneous

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- [The 95th and 99th percentiles are the most crucial application metrics](https://medium.com/@vikaskumar4793/the-95th-and-99th-percentiles-are-the-most-crucial-application-metrics-33085d2d3e34)
- [What are 99 percentile and 95 percentile?](https://www.googlecloudcommunity.com/gc/Apigee/What-are-99-percentile-and-95-percentile/td-p/67052)

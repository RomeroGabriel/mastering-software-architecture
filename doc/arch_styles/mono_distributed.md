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

In monolithic architectures, `bandwidth is typically not a concern because processing within a monolith often requires little to no additional bandwidth`. However, in distributed systems, `communication between services can consumes significant bandwidth, which can lead to network slowdowns`.

When a service needs to connect to other services to process requests, it consumes bandwidth. This can become problematic, especially if these requests occur frequently. This situation, known as `stamp coupling`, can have a significant impact on bandwidth usage. `To address stamp coupling in distributed architectures, there are several approaches you can consider`:

1. Create private RESTful API endpoints.
1. Use field selectors in the contract.
1. Adopt GraphQL to decouple contracts.
1. Combine value-driven contracts with consumer-driven contracts (CDCs).
1. Leverage internal messaging endpoints.

!!! tip
    No matter which approach you choose, `the key is to minimize the amount of data transferred between services or systems in a distributed architecture`. This is essential for addressing the fallacy of infinite bandwidth.

### The Network Is Secure

In the world of distributed computing, it's common for architects and developers to rely on tools like virtual private networks (VPNs), trusted networks, and firewalls, which can create a false sense of security. However, `it's crucial to remember that the network itself is not inherently secure`.

`Security becomes a much more complex challenge in distributed architectures`. In such systems, `every endpoint, associated with each distributed deployment unit, must be diligently secured to prevent unauthorized or malicious requests from reaching those services`. As you transition from a monolithic to a distributed architecture, the potential surface area for security threats and attacks increases significantly.

`Ensuring the security of every endpoint, even during interservice communication, is a demanding task`. This is one of the reasons why `synchronous`, highly-distributed architectures like microservices or service-based architecture often exhibit slower performance. The need to address security at every level introduces additional overhead and complexity.

### The Topology Never Changes

This fallacy `assumes that the overall network structure`, including routers, hubs, switches, firewalls, and other network components, remains static and `never undergoes changes. However, in reality, network topologies can and do change`.

`Architects should recognize that network topologies are dynamic` and may evolve over time. `It's crucial for architects to maintain open communication with network administrators and operations teams to stay informed about any changes to the network infrastructure`. This awareness allows architects to adapt and make necessary adjustments to ensure the reliability and performance of distributed systems, minimizing unwelcome surprises.

### There Is Only One Administrator

Architects often make the `mistake of assuming they only need to collaborate and communicate with a single administrator when dealing with network issues`. This fallacy `highlights the complexity of distributed architecture and the need for extensive coordination`.

`In distributed architectures, effective communication and collaboration with multiple administrators are essential`. Unlike monolithic applications, where a single deployment unit simplifies administration, distributed systems require architects to engage with various network administrators to ensure everything functions correctly.

### Transport Cost Is Zero

The term `transport cost` in this context doesn't refer to how quickly data travels, but to the `actual expenses incurred when making what seems like a simple RESTful call.` Architects often mistakenly assume that the existing infrastructure is enough for such calls or for breaking down a monolithic application. However, this isn't usually the case.

`Distributed architectures typically come with significantly higher expenses compared to monolithic ones`. This increase in cost is primarily due to the need for extra hardware, servers, gateways, firewalls, the creation of new subnets, proxies, and other resources.

When architects dive into `designing a distributed architecture, it's essential to thoroughly assess the current server and network infrastructure`. This assessment should consider factors like capacity, bandwidth, latency, and security zones. By doing this, architects can avoid being caught off guard by unexpected costs and plan more effectively.

### The Network Is Homogeneous

Many architects and developers often assume that networks are homogeneous, consisting of hardware from a single vendor. In reality, `most companies have a mix of network hardware vendors in their infrastructure, and sometimes, even more than that`. The importance of this fallacy lies in the fact that `not all of these diverse hardware vendors seamlessly cooperate with one another`. While most components work together, questions arise about the seamless integration of Juniper hardware with Cisco hardware, for instance.

`While networking standards have progressed over the years, reducing this problem, the fact remains that not all scenarios, loads, and circumstances have been thoroughly tested`. Consequently, network packets can occasionally get lost, causing issues.

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- [The 95th and 99th percentiles are the most crucial application metrics](https://medium.com/@vikaskumar4793/the-95th-and-99th-percentiles-are-the-most-crucial-application-metrics-33085d2d3e34)
- [What are 99 percentile and 95 percentile?](https://www.googlecloudcommunity.com/gc/Apigee/What-are-99-percentile-and-95-percentile/td-p/67052)

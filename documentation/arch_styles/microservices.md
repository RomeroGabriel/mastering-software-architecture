# Microservices Architecture Style

## History

Microservices differs in this regard—it was namewd fairly early in its usage and popularized by a famous blog entry by Martin Fowler and James Lewis entitled [Microservices](https://martinfowler.com/articles/microservices.html), published in March 2014. They recognized many common characteristics in this relatively new architectural style and delineated them.

`A significant influence on microservices comes from domain-driven design (DDD)`, a logical design process for software projects. One key concept from DDD, known as [bounded context](#bounded-context), played a decisive role in inspiring microservices.

### Reuse, Trade-Offs and First Law of Software Architecture

While reuse holds clear advantages, it's crucial to remember the First Law of Software Architecture, which emphasizes trade-offs. `The negative trade-off of reuse is increased coupling`. When architects design a `system to prioritize reuse, they inherently introduce coupling, whether through inheritance or composition`.

`In scenarios where the architect's goal emphasizes high degrees of decoupling, microservices favor duplication over reuse`. The central objective of microservices is to achieve a high level of decoupling, aligning with the logical notion of bounded context from domain-driven design.

## Topology

In the realm of microservices, `the architectural topology is characterized by the small size and single-purpose nature of each service`. Unlike other distributed architectures, `microservices envision services as standalone entities, each encapsulating all the essential components needed for independent operation, including databases and other dependencies`.

!!! example
    ![The topology of the microservices architecture style from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microservices_arch_example.png)
    > The topology of the microservices architecture style from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

## Distributed

Microservices constitute a distributed architecture, `where each service operates in its independent process`. Initially tied to physical machines, `this concept has evolved to embrace virtual machines and containers`. The extensive decoupling of services in a distributed environment addresses common challenges in architectures featuring multitenant infrastructure, `offering operational advantages such as efficient resource utilization and improved isolation`.

`While this distributed approach brings benefits, it also introduces performance considerations`. `Network calls` inherently take longer than local method calls, and `security verification at each endpoint` adds processing time. Consequently, architects must carefully consider granularity when designing a system to mitigate these implications.

One notable aspect of microservices is the `reluctance to employ transactions across service boundaries`. Seasoned architects emphasize the `importance of determining the appropriate granularity for services` as a key factor in achieving success within this architecture.

## Bounded Context

`The bounded context concept embodies a decoupling strategy`. In the context of software development, when a developer defines a domain, `that domain includes many entities and behaviors reflected in artifacts such as code and database schemas`.

!!! example
    An application might have a domain named `CatalogCheckout`, encompassing elements like catalog items, customers, and payment.

`In a traditional monolithic architecture, developers commonly share these concepts, creating reusable classes and interconnected databases`. In a bounded context, however, `internal components, like code and data schemas, are tightly coupled to accomplish their work but remain decoupled from anything outside the bounded context`, such as a database or class definition from another bounded context. This allows each context to define only what it requires without being influenced by other constituents.

`Microservices architecture revolves around the core concept of bounded context, where each service encapsulates a specific domain or workflow`. This approach aims to include everything essential for a service to operate independently within the application, `discouraging unnecessary coupling and emphasizing duplication over shared resources`.

### Granularity

Determining the `appropriate granularity for services` in microservices poses a common challenge for architects. `Oversimplifying by creating overly small services can lead to increased communication links between services, impacting overall system efficiency`. `Striking the right balance is crucial for achieving effective communication and collaboration among services`.

Applications may have naturally expansive boundaries for certain segments, `acknowledging that certain business processes exhibit higher levels of coupling than others is essential`. Architects can navigate this challenge by adhering to guidelines that assist in identifying the most suitable boundaries for effective microservices implementation :

!!! info "Purpose"
    Microservices should ideally `exhibit high functional cohesion, representing a distinct and significant behavior contributing to the overall application`.

!!! info "Transactions"
    `Minimizing reliance on transactions enhances the robustness of distributed architectures`.Bounded contexts are business workflows, and often `entities cooperating in transactions can guide architects in defining suitable service boundaries`.

!!! info "Choreography"
    Architectures that balance domain isolation with communication requirements might benefit from `bundling services back into larger entities to mitigate communication overhead, in cases when multiple services require extensive communications`.

`Iterative refinement is essential for achieving optimal service design`. Architects rarely achieve the perfect granularity, data dependencies, and communication styles on the initial attempt. `Continuous iteration and refinement increase the likelihood of developing a well-tailored and efficient microservices architecture`.

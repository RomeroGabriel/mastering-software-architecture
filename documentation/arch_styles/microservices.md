# Microservices Architecture Style

## History

Microservices differs in this regard—it was namewd fairly early in its usage and popularized by a famous blog entry by Martin Fowler and James Lewis entitled [Microservices](https://martinfowler.com/articles/microservices.html), published in March 2014. They recognized many common characteristics in this relatively new architectural style and delineated them.

`A significant influence on microservices comes from domain-driven design (DDD)`, a logical design process for software projects. One key concept from DDD, known as `bounded context`, played a decisive role in inspiring microservices.

### Bounded Context

`The bounded context concept embodies a decoupling strategy`. In the context of software development, when a developer defines a domain, `that domain includes many entities and behaviors reflected in artifacts such as code and database schemas`.

!!! example
    An application might have a domain named `CatalogCheckout`, encompassing elements like catalog items, customers, and payment.

`In a traditional monolithic architecture, developers commonly share these concepts, creating reusable classes and interconnected databases`. In a bounded context, however, `internal components, like code and data schemas, are tightly coupled to accomplish their work but remain decoupled from anything outside the bounded context`, such as a database or class definition from another bounded context. This allows each context to define only what it requires without being influenced by other constituents.

### Reuse, Trade-Offs and First Law of Software Architecture

While reuse holds clear advantages, it's crucial to remember the First Law of Software Architecture, which emphasizes trade-offs. `The negative trade-off of reuse is increased coupling`. When architects design a `system to prioritize reuse, they inherently introduce coupling, whether through inheritance or composition`.

`In scenarios where the architect's goal emphasizes high degrees of decoupling, microservices favor duplication over reuse`. The central objective of microservices is to achieve a high level of decoupling, aligning with the logical notion of bounded context from domain-driven design.

## Topology

In the realm of microservices, `the architectural topology is characterized by the small size and single-purpose nature of each service`. Unlike other distributed architectures, `microservices envision services as standalone entities, each encapsulating all the essential components needed for independent operation, including databases and other dependencies`.

!!! example
    ![The topology of the microservices architecture style from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microservices_arch_example.png)
    > The topology of the microservices architecture style from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

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

### Data Isolation

Microservices necessitates a focus on data isolation, an aspect that distinguishes it from other architecture styles that rely on a single database for persistence. `In the pursuit of minimal coupling, microservices avoids shared schemas and databases functioning as integration points`.

When determining service granularity, architects must be cautious of falling into the [entity trap](../components/index.md#component-design) and `resist the temptation to simply model their services to resemble single entities in a database`.

`Unlike conventional practices of utilizing relational databases for consolidating values within a system to establish a single source of truth`, microservices, with its distributed nature, poses a challenge in maintaining this approach. Architects are tasked with `deciding how to address this issue: designating one domain as the source of truth for specific information and coordinating with it for value retrieval, or employing database replication or caching for information distribution`.

While this level of data isolation may present challenges, it also opens avenues for `flexibility`. With teams no longer compelled to converge on a single database, `each service can opt for the most suitable tool` based on factors such as cost, storage type, and other considerations. In a highly decoupled system, teams enjoy the advantage of `adapting their choices without affecting other teams, as coupling to implementation details is prohibited`.

## API Layer

In the microservices paradigm, diagrams often feature an `API layer positioned between the system's consumers` (user interfaces or calls from other systems), `although its inclusion is optional`. While the API layer serves various purposes, `it should not function as a mediator or orchestration tool` if architects intend to adhere to the fundamental philosophy of this architecture. According to this philosophy, `all significant logic within microservices should take place within a bounded context`, and introducing orchestration or similar logic in a mediator would violate this principle.

This also illustrates the `difference between technical and domain partitioning in architecture`: architects typically use `mediators in technically partitioned architectures`, whereas `microservices is firmly domain partitioned`.

## Operational Reuse

In the microservices paradigm, `where duplication is favored over coupling`, architects face the challenge of `handling operational concerns that traditionally benefit from coupling`, such as monitoring, logging, and circuit breakers. Unlike the traditional service-oriented architecture philosophy, which promotes reusing both domain and operational functionality, microservices endeavors to separate these two concerns.

As teams build multiple microservices, they recognize `common elements that could benefit from a shared approach`. The [sidecar](https://learn.microsoft.com/en-us/azure/architecture/patterns/sidecar) pattern emerges as a solution to this challenge. `Operational concerns are encapsulated within each service as a distinct component`, owned either by individual teams or a centralized infrastructure team. `This sidecar component efficiently manages all operational aspects that teams find advantageous to couple together`. Consequently, when updates or upgrades are needed, the shared infrastructure team can seamlessly update the sidecar, ensuring that each microservice receives the new functionality.

`The sidecar pattern not only addresses the challenge of common operational concerns but also facilitates the creation of a` [service mesh](https://www.redhat.com/en/topics/microservices/what-is-a-service-mesh). This mesh allows for centralized control across the architecture for vital concerns like logging and monitoring. `The individual sidecar components connect to form a cohesive operational interface, creating a unified experience across all microservices`. Each microservice functions as a node within this mesh, offering a console for global control over operational coupling, including monitoring levels, logging, and other cross-cutting operational considerations.

`Service discovery plays a crucial role in achieving elasticity in microservices architectures`. Instead of directly invoking a single service, `requests are routed through a service discovery tool, which monitors request patterns and can scale or spin up new service instances as needed`. `Architects often integrate service discovery into the service mesh, making it an integral part of every microservice`. The API layer is frequently utilized to host service discovery, providing a centralized location for user interfaces or other calling systems to discover and create services in a flexible and consistent manner.

## Frontends

Microservices prioritize decoupling, `aiming to extend this separation to both backend and user interface concerns`. While the `original vision of microservices included the user interface as part of the bounded context` in alignment with Domain-Driven Design (DDD) principles, `practical considerations, particularly in web applications, have presented challenges to fully realizing this goal`. As a result, two predominant styles of user interfaces have emerged in microservices architectures.

The first style involves a `monolithic frontend`, where a `single user interface interacts with the backend through the API layer` to fulfill user requests. This frontend can take various forms, such as a rich desktop application, mobile app, or web application. For instance, many modern web applications utilize JavaScript web frameworks to construct a unified user interface.

The second option for user interfaces adopts `microfrontends, leveraging components at the user interface level to achieve a level of granularity and isolation in sync with the backend services`. In this approach, `each service emits its own user interface`, and the frontend coordinates with these emitted user interface components. This pattern allows teams to establish clear service boundaries from the user interface to the backend services, promoting unity within a single team across the entire domain.

## Communication

In microservices, the `challenge of determining appropriate granularity impacts both data isolation and communication, influencing how services remain decoupled while still coordinating effectively`.

At its core, architects must make a `fundamental decision regarding synchronous or asynchronous communication`. Synchronous communication entails the caller waiting for a response from the callee. Microservices architectures typically employ `protocol-aware heterogeneous interoperability`.

!!! Info "Protocol-Aware, Heterogeneous and Interoperability"
    **Protocol-aware**

    Because microservices lack a centralized integration hub to avoid operational coupling, `each service should understand how to call other services`. As a result, `architects often standardize on specific protocols for inter-service communication`, such as a level of REST, message queues, and so forth. This implies that services must be aware of (or discover) the protocol to use when calling other services.

    **Heterogeneous**

    `Each service may be developed in a different technology stack`. Embracing heterogeneity signifies that microservices fully supports polyglot environments, where various services utilize different platforms.

    **Interoperability**

    `Describing services calling one another`, interoperability in microservices aims to discourage transactional method calls while `promoting network-based communication`.

For `asynchronous` communication, architects often leverage `events and messages`, resulting in an internal [event-driven architecture](event_driven_arch.md#event-driven-architecture-style). In microservices, the broker and mediator patterns manifest as choreography and orchestration.

### Choreography and Orchestration

`Choreography in microservices utilizes the communication style of a` [broker event-driven architecture](event_driven_arch.md#broker-topology). Unlike architectures with a central coordinator, `choreography adheres to the bounded context philosophy`, promoting the implementation of decoupled events between services. In this approach, `each service independently calls others as needed, without relying on a central mediator`.

??? example "Choreography"
    Suppose a user requests details about a wish list, and the `CustomerWishList` service lacks essential information. In choreography, it would make a `direct call to CustomerDemographics to retrieve the missing data`, delivering the result back to the user.

    ![Using choreography in microservices to manage coordination from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microservices_choreography_example.png)
    > Using choreography in microservices to manage coordination from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

Because microservices architectures `lacks a global mediator` like in some service-oriented architectures, `allow architects to create localized mediators when coordination across multiple services is necessary`. Developers can design a `service dedicated to coordinating specific calls, such as obtaining comprehensive customer information`. Users then interact with this mediator service, which, in turn, communicates with the required services.

??? example "Orchestration"
    ![Using orchestration in microservices from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microservices_orchestration_example.png)
    > Using orchestration in microservices from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

The First Law of Software Architecture acknowledges that `neither choreography nor orchestration is flawless—each comes with trade-offs`. In choreography, architects uphold the highly decoupled philosophy of the architecture, maximizing the benefits it offers. However, `handling common challenges like error management and coordination becomes more intricate in choreographed environments`.

In scenarios involving complex workflows, `the initial service called may need to act as a mediator, coordinating interactions across a range of other services`. This pattern, known as the `front controller pattern`, transforms a nominally choreographed service into a more complex mediator. `The drawback lies in the increased complexity within the service`.

??? example "Complex Choreography"

    ![Using choreography for a complex business process from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microservices_choreography_complex_example.png)
    > Using choreography for a complex business process from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

On the other hand, `architects may opt for orchestration in handling intricate business processes`. `By constructing a mediator, architects manage the complexity and coordination required for the business workflow`. While this `introduces coupling between services`, it enables architects to concentrate coordination efforts into a single service, minimizing the impact on others. Often, `domain workflows inherently involve some level of coupling, challenging architects to represent that coupling in ways that align with both domain and architectural objectives`.

??? example "Complex Orchestration"
    ![Using orchestration in microservices from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microservices_orchestration_complex_example.png)
    > Using orchestration in microservices from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

### Transactions and SAGAS

Architects in the realm of microservices `looks for extreme decoupling`, but they often grapple with the `challenge of coordinating transactions across services`. The same level of decoupling that characterizes the architecture, especially in terms of databases, `complicates achieving the atomicity that was once straightforward in monolithic applications`.

`Constructing transactions that span service boundaries contradicts the fundamental decoupling principle of microservices and introduces a form of dynamic connascence, the worst known connascence`, [the connascence of value](../modularity/measuring.md#dynamic-connascence). The foremost advice for architects contemplating transactions across services is unequivocal: avoid it! Instead, address the granularity of components. Transaction boundaries often serve as a key indicator of service granularity.

!!! danger
    The foremost advice for architects contemplating transactions across services is unequivocal: `avoid it!` Instead, `address the granularity of components.` Transaction boundaries often serve as a key indicator of service granularity.

!!! tip
    Don’t do transactions in microservices. `Fix granularity instead!`

For services that still demanding transactional coordination, `there are patterns available to manage transaction orchestration, with significant trade-offs`.

One prevalent distributed transactional pattern in microservices is the [saga pattern](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/saga/saga). In this approach, `a service assumes the role of a mediator, orchestrating multiple service calls and coordinating the transaction`. The mediator initiates each part of the transaction, logs success or failure, and manages the overall outcome. `If everything proceeds as planned, all values in the services and their associated databases update synchronously`.

??? example
    ![The saga pattern in microservices architecture from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microservices_saga_example.png)
    > The saga pattern in microservices architecture from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

`In the event of an error, the mediator ensures that no part of the transaction succeeds if another part fails`. If the initial part succeeds but the subsequent part encounters a failure, the mediator `sends a request to all successful parts, instructing them to undo their previous actions`. This style of transactional coordination is known as a `compensating transaction framework`. Typically, developers implement this pattern by `placing each mediator-initiated request in a pending state until the overall success is signaled by the mediator`. However, this design `complexity intensifies when dealing with asynchronous requests`, especially if new requests depend on pending transactional states. It also results in `increased coordination traffic at the network level`.

??? example
    ![Saga pattern compensating transactions for error conditions from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microservices_saga_error_example.png)
    > Saga pattern compensating transactions for error conditions from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

An alternative implementation of a compensating transaction framework involves developers creating both `do` and `undo` operations `for each potentially transactional operation`. While this approach reduces coordination during transactions, `the undo operations tend to be considerably more complex` than their counterpart do operations, essentially doubling the effort required for design, implementation, and debugging.

While architects can technically build transactional behavior across services, doing so `contradicts the core rationale behind choosing the microservices pattern`. While exceptions may arise, the overarching advice for architects is to use the saga pattern judiciously.

!!! tip
    A few transactions across services may be necessary, but if they dominate the architecture, it indicates potential mistakes in the design!

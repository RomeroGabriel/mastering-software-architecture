# Scope of Architecture Characteristics

In the past, within the realm of software architecture, `the scope of architecture characteristics was traditionally placed at the system level`. For instance, scalability was discussed with the entire system in mind, as most systems were monolithic. However, `this is no longer accurate today`, as the field has evolved, exemplified by the emergence of microservices.

There are various `code-level metrics` that enable architects to analyze the structural aspects of an architecture. However, these metrics often offer insights into low-level code specifics, `rather than the entirety of a system's components`. For example, databases can significantly influence various architecture characteristics, particularly operational ones. Code performance won't matter if the database doesn't scale.

Architects must also consider `external components beyond the codebase that can influence these characteristics`. Furthermore, it's crucial to measure these types of dependencies.

## Architectural Quanta and Granularity

To define the architecture quantum, we needed a measure of how components are “wired” together, which corresponds to the [connascence](../modularity/measuring.md#connascence) concept. Connascence map dependencies between components, classifying them between [static connascence](../modularity/measuring.md#static-connascence) or [dynamic connascence](../modularity/measuring.md#dynamic-connascence).

The definition about architecture quantum is:

> An independently deployable artifact with high functional cohesion and synchronous connascence

??? info "Independently deployable"
    An architectural quantum is a `self-sufficient unit that includes everything needed to work on its own within the larger architecture`. For instance, if an application relies on a database, the database is considered part of this self-contained unit because the application can't function without it..

??? info "High functional cohesion"
    Functional cohesion in component design `measures how well the code within a component serves a single, meaningful purpose`.
    In microservices architectures, high functional cohesion is particularly important because each service is typically designed to handle a specific workflow or function, ensuring clarity and efficiency in the system's organization.

??? info "Synchronous connascence"
    Synchronous connascence `refers to synchronous calls within an application context or between distributed services within an architecture quantum`.
    In a microservices architecture, when one service calls another synchronously, it's crucial that both services have similar operational architecture characteristics. If there's a significant difference in scalability between the caller and callee, issues like timeouts and reliability problems may arise.

The concept of `architecture quantum provides the new scope for architecture characteristics`. In modern systems, `architects define these characteristics at the quantum level/specific parts`, rather than at the system level/whole system.  By `focusing on a more specific scope for essential operational concerns, architects can detect architectural challenges early`, which can lead to the development of hybrid architectures.

### Choosing Between Monolithic x Distributed Architectures

The choice between a monolithic and distributed architecture `depends on the scope of architecture characteristics`. A monolithic architecture consists of a single deployable unit that contains all system functionality and is typically connected to a single database. In contrast, a distributed architecture involves multiple services running independently, communicating through networking protocols.

The decision hinges on how many architecture quanta are discovered during the design process. `If the system can function effectively with a single quantum (meaning one set of architecture characteristics), a monolithic architecture is advantageous`. However, `if different components require distinct architecture characteristics, a distributed architecture` is necessary to accommodate these variations.

The ability to make this fundamental architectural decision early in the design process underscores the benefits of using the architecture quantum to analyze architecture characteristics' scope and coupling.

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

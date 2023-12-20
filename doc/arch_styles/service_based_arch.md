# Service-Base Architecture Style

Service-based architecture represents a `hybrid approach that combines elements of the microservices architecture style`. This pragmatic architectural style is known for its flexibility, making it a popular choice for various business applications. `Despite being a distributed architecture, it offers a balance between complexity and cost` when compared to more intricate distributed styles like microservices or event-driven architecture, making it a very popular choice for many business-related applications.

## Topology

`The structure of service-based architecture is like a distributed system with different layers`. It includes a user interface that's deployed separately, bigger independent services, and a central database that holds everything together.

In this style, the `services, which are like big chunks of the application, are called domain services. These services operate autonomously and are separately deployed. They share one big database`. There are usually 4 to 12 of these services in one application.

![Basic topology of the service-based architecture style [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/arch_styles/service-base-arch.png)
> Basic topology of the service-based architecture style [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

While a service-based architecture `usually maintains only a single instance of each domain service, multiple instances can exist` based on scalability, fault tolerance, and throughput requirements. `Multiple instances of a service necessitate load-balancing capabilities between the user interface and the domain service` to ensure the interface connects to a healthy and available service instance.

`Services are accessed remotely from a user interface through different ways like REST, messaging, or  remote procedure call (RPC)`. While an API layer with a proxy or gateway can be employed to access services, in most cases, the user interface interacts directly with the services.

`One important thing here is that all these services use the same database`. This means they can utilize SQL queries and joins akin to traditional monolithic layered architectures. Given the limited number of services, `database connections typically pose no issues in service-based architecture. However, database alterations can present challenges`.

### Topology Variants

Within the service-based architecture style, various topology variants exist, making it one of the most adaptable styles.

??? example "Broken User Interface"
    ![User interface variants from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/arch_styles/service-base-arch-example2.png)
    > User interface variants from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

??? example "Multiple Databases"
    Dividing a single monolithic database into `separate databases, sometimes even establishing domain-specific databases that match each domain service`, similar to how it's done in microservices. `The key here is to ensure that each separate database doesn't contain data needed by another domain service. This approach prevents the need for communication between domain services (something to avoid in service-based architecture) and avoids duplicating data across databases`.

    ![Database variants from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/arch_styles/service-base-arch-example3.png)
    > Database variants from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

??? example "API Layer"
    Another possibility is to introduce an `API layer, comprising a reverse proxy or gateway between the user interface and services`. This practice is `beneficial when exposing domain service functions to external systems or consolidating shared cross-cutting concerns`, moving them outside the user interface. Such concerns might include managing metrics, security, auditing requirements, and service discovery.

    ![Adding an API layer between the user interface and domain services from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/arch_styles/service-base-arch-example4.png)
    > Adding an API layer between the user interface and domain services from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

## Service and Granularity

`In a service-based architecture, domain services are generally designed with a coarse-grained approach`. Typically, each domain service includes an API facade layer, a business layer, and a persistence layer. An alternative design approach involves dividing each domain service into sub-domains, similar to the modular monolith architecture style.

??? note "Coarse-grained approach vs Fine-grained approach"
    In software architecture, a coarse-grained approach refers to the use of larger, more encompassing components or services that handle multiple tasks or operations as a single unit. On the other hand, a fine-grained approach involves the use of smaller, more specialized components or services, each responsible for specific and often singular tasks or operations.

`Irrespective of the design, every domain service must incorporate an API access facade that interacts with the user interface, managing the execution of various business functionalities`.

!!! example
    For example, within the OrderService domain service, the API access facade orchestrates a business request, such as placing an order, processing payments, and updating product inventory for each item ordered. `This orchestration, which involves several tasks within a single service, differs from the orchestration of numerous distinct remote services in the microservices architecture style`.

`Due to their coarse-grained nature, domain services in a service-based architecture rely on regular ACID within a single service`. In contrast, highly distributed architectures like microservices, with their `fine-grained services, utilize a distributed transaction technique known as BASE transactions`.

!!! note "BASE transactions x ACID transactions"
    These `BASE transactions (basic availability, soft state, eventual consistency) prioritize eventual consistency over strict database integrity`, distinguishing them from `ACID transactions (atomicity, consistency, isolation, durability) database transactions to maintain database integrity` in a service-based architecture.

This disparity highlights a `key difference between internal class-level orchestration and external service orchestration, emphasizing the divergence in granularity between service-based architecture and microservices`.

Although `coarse-grained domain services ensure robust data integrity and consistency`, they involve trade-offs. `Implementing changes to a functionality in service-based architecture necessitates testing the entire service, while in microservices, it only affects a small service without impacting others`.

## Database Partitioning

In a service-based architecture, `services often share a single/monolithic database`, primarily due to the small number of services within an application. `This database coupling, can bring challenges, especially concerning database table schema modifications`. Improper schema changes can potentially impact every service, rendering `database alterations costly in terms of effort and coordination`.

`The shared class files representing database table schemas (referred to as entity objects) typically reside in a custom shared library used by all domain services`. However, `employing a single shared library of entity objects can be less effective in this context`.

!!! danger "The problem with single shared library"
    Any alterations to the database table structures necessitate changes to the shared library, demanding **`redeployment across all services, regardless of their direct use of the modified table`**. While shared library versioning can aid in managing this issue, comprehending the actual impact on services without detailed analysis remains challenging.

`A practical solution to mitigate the effects of database changes involves logically partitioning the database and reflecting this partitioning through federated shared libraries`.

!!! example "Using partitioning database and libraries"
    For instance, logical partitioning can be executed by `segmenting the database into distinct domains (such as common, customer, invoicing, order, and tracking), with corresponding shared libraries matching these partitions`. Employing this technique `ensures that changes made to a specific table within a particular domain only affect services associated with that partition`.
    `It's also possible to have a common domain with a common shared library used by all services`. `These tables are shared across all services`, and any changes to these tables require coordination among all services accessing the shared database.

    ![Using multiple shared libraries for database entity objects from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/arch_styles/service-base-arch-example-db.png)
    > Using multiple shared libraries for database entity objects from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

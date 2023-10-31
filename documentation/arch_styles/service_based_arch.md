# Service-Base Architecture Style

Service-based architecture represents a `hybrid approach that combines elements of the microservices architecture style`. This pragmatic architectural style is known for its flexibility, making it a popular choice for various business applications. `Despite being a distributed architecture, it offers a balance between complexity and cost` when compared to more intricate distributed styles like microservices or event-driven architecture, making it a very popular choice for many business-related applications.

## Topology

`The structure of service-based architecture is like a distributed system with different layers`. It includes a user interface that's deployed separately, bigger independent services, and a central database that holds everything together.

In this style, the `services, which are like big chunks of the application, are called domain services. These services operate autonomously and are separately deployed. They share one big database`. There are usually 4 to 12 of these services in one application.

![Basic topology of the service-based architecture style [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/service-base-arch.png)
> Basic topology of the service-based architecture style [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

While a service-based architecture `usually maintains only a single instance of each domain service, multiple instances can exist` based on scalability, fault tolerance, and throughput requirements. `Multiple instances of a service necessitate load-balancing capabilities between the user interface and the domain service` to ensure the interface connects to a healthy and available service instance.

`Services are accessed remotely from a user interface through different ways like REST, messaging, or  remote procedure call (RPC)`. While an API layer with a proxy or gateway can be employed to access services, in most cases, the user interface interacts directly with the services.

`One important thing here is that all these services use the same database`. This means they can utilize SQL queries and joins akin to traditional monolithic layered architectures. Given the limited number of services, `database connections typically pose no issues in service-based architecture. However, database alterations can present challenges`.

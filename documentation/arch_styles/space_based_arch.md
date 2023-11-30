# Space-Based Architecture Style

The space-based architecture style is crafted to tackle `challenges related to high scalability, elasticity, and concurrent user demands`. `It proves beneficial for applications dealing with variable and unpredictable concurrent user volumes`. Architecturally addressing extreme scalability issues is often more effective than attempting to scale out a database or retrofit caching technologies into a non-scalable architecture.

In high-volume applications with significant concurrent user loads, the `database typically becomes the ultimate bottleneck, limiting the number of transactions processed concurrently`. Despite the assistance of various caching technologies and database scaling products, scaling out a conventional application for extreme loads remains a challenging task.

??? example "Web-Based Bussiness"
    In web-based businesses, the usual flow involves a `request from a browser hitting the web server, then an application server, and finally, the database server`. This works well for a small user group, but as `users increase, bottlenecks emerge at each layer`—first at the web server, then the application server, and finally, the database server. `Scaling out web servers is a common response, but it often shifts the bottleneck to the application server, which is more complex and costly to scale`. Even if the database is scaled (and even more costly to scale), the result is a `triangle-shaped topology`, with web servers being the easiest to scale and the database the hardest.
    ![Scalability limits within a traditional web-based topology from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/space-based-web-based-example.png)
    > Scalability limits within a traditional web-based topology from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

## General Topology

Space-based architecture is rooted in the concept of `tuple space`, utilizing multiple parallel processors communicating through shared memory. `It achieves high scalability, elasticity, and performance by eliminating the central database as a synchronous constraint`. Instead, it relies on replicated in-memory data grids.

??? quote "Tuple Space"
    A tuple space is an implementation of the associative memory paradigm for parallel/distributed computing. It provides a repository of tuples that can be accessed concurrently. As an illustrative example, consider that there are a group of processors that produce pieces of data and a group of processors that use the data. Producers post their data as tuples in the space, and the consumers then retrieve data from the space that match a certain pattern. This is also known as the blackboard metaphor. Tuple space may be thought as a form of distributed shared memory. [Wikipedia link](https://en.wikipedia.org/wiki/Tuple_space)

`Application data is stored in-memory and replicated across all active processing units`. `When a unit updates data, it asynchronously sends it to the database via messaging with persistent queues`. Processing units dynamically start and shut down based on `user load`, addressing `variable scalability`. `With no central database bottleneck, near-infinite scalability is achieved`.

Key components include processing units with application code, virtualized middleware for unit management, data pumps for asynchronous data updates to the database, data writers for database updates, and data readers delivering database data to processing units on startup.

!!! example
    ![Space-based architecture basic topology from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/space-based-basic-topology.png)
    > Space-based architecture basic topology from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

### Processing Unit

The processing unit (as shown in the example image), `encompasses the application logic, both web-based components and backend business logic`. Its content varies depending on the application type. Smaller web-based apps might reside in a single processing unit, while larger ones may distribute functionality across multiple units based on application areas. The processing unit may also host small, single-purpose services (akin to microservices). `Alongside the application logic, it integrates an in-memory data grid and replication engine`, often implemented using products like Hazelcast, Apache Ignite, or Oracle Coherence.

### Virtualized Middleware

The virtualized middleware `manages architecture infrastructure, overseeing data synchronization and request handling`. It comprises components like a `messaging grid`, `data grid`, `processing grid`, and `deployment manager`.

!!! info "Messaging Grid"
    The messaging grid `oversees input requests and session state`. Upon receiving a request, `it identifies available processing units and directs the request to one of them`. The complexity can range depending on the algorithm used from simple `round-robin` to `next-available`, `managed by a web server with load-balancing capabilities` (e.g., HA Proxy, Nginx).

!!! info "Data Grid"
    The data grid stands out as a `pivotal component` in this architecture style. In modern implementations, `it resides within processing units as a replicated cache`. However, when setups `requiring an external controller or using a distributed cache, this functionality extends to both processing units and the virtualized middleware's data grid component`. As the messaging grid can route requests to any available processing unit, `maintaining identical data in each unit's in-memory grid is crucial`. Despite the synchronous data replication illustration below, actual synchronization is asynchronous and rapid, typically finishing in under 100 milliseconds.

    ![Data grid from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/space-based-data-grid.png)
    > Data grid from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

    `Data synchronization occurs among processing units that share the same named data grid`. For instance, consider an internal replicated data grid in processing units containing customer profile information, using Hazelcast. C`hanges made to the CustomerProfile named cache in any processing unit replicate to all others with the same named cache`. `Each processing unit can hold multiple replicated caches as needed or request data from another unit (choreography) or leverage the processing grid for orchestration`.

    Data replication within processing units enables service instances to `start and stop without requiring data retrieval from the database, as long as one instance holds the named replicated cache`. When a processing unit instance starts, it connects to the cache provider (like Hazelcast), requests the named cache, and loads it from another instance.

    `Each processing unit is aware of all others (including themselves) through a member list`, containing the IP addresses and ports of units `using the same named cache`. Suppose instance 1 receives a request to update customer profile information; `when it updates the cache, the data grid (e.g., Hazelcast) asynchronously updates other replicated caches, ensuring consistent synchronization`. `If processing unit instances go down, all others are automatically updated to reflect the lost member`.

!!! info "Processing Grid"
    The processing grid, an `optional element in virtualized middleware`, oversees `coordinated request processing when multiple processing units are involved in a single business request`. If a request necessitates coordination between different processing unit types (e.g., an order processing unit and a payment processing unit), `the processing grid mediates and orchestrates the request between these units`.

!!! info "Deployment Manager"
    The deployment manager component oversees the `dynamic startup and shutdown of processing unit instances based on load conditions`. Continually monitoring response times and user loads, it starts up new processing units with increased load and shuts down units during decreased load. `This critical component ensures variable scalability (elasticity) within an application`.

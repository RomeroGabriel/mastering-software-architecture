# Space-Based Architecture Style

The space-based architecture style is crafted to tackle `challenges related to high scalability, elasticity, and concurrent user demands`. `It proves beneficial for applications dealing with variable and unpredictable concurrent user volumes`. Architecturally addressing extreme scalability issues is often more effective than attempting to scale out a database or retrofit caching technologies into a non-scalable architecture.

In high-volume applications with significant concurrent user loads, the `database typically becomes the ultimate bottleneck, limiting the number of transactions processed concurrently`. Despite the assistance of various caching technologies and database scaling products, scaling out a conventional application for extreme loads remains a challenging task.

!!! example "Web-Based Bussiness"
    In web-based businesses, the usual flow involves a `request from a browser hitting the web server, then an application server, and finally, the database server`. This works well for a small user group, but as `users increase, bottlenecks emerge at each layer`—first at the web server, then the application server, and finally, the database server. `Scaling out web servers is a common response, but it often shifts the bottleneck to the application server, which is more complex and costly to scale`. Even if the database is scaled (and even more costly to scale), the result is a `triangle-shaped topology`, with web servers being the easiest to scale and the database the hardest.
    ![Scalability limits within a traditional web-based topology from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/space-based-web-based-example.png)
    > Scalability limits within a traditional web-based topology from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

## General Topology

Space-based architecture is rooted in the concept of `tuple space`, utilizing multiple parallel processors communicating through shared memory. `It achieves high scalability, elasticity, and performance by eliminating the central database as a synchronous constraint`. Instead, it relies on replicated in-memory data grids.

??? quote "Tuple Space"
    A tuple space is an implementation of the associative memory paradigm for parallel/distributed computing. It provides a repository of tuples that can be accessed concurrently. As an illustrative example, consider that there are a group of processors that produce pieces of data and a group of processors that use the data. Producers post their data as tuples in the space, and the consumers then retrieve data from the space that match a certain pattern. This is also known as the blackboard metaphor. Tuple space may be thought as a form of distributed shared memory. [Wikipedia link](https://en.wikipedia.org/wiki/Tuple_space)

`Application data is stored in-memory and replicated across all active processing units`. `When a unit updates data, it asynchronously sends it to the database via messaging with persistent queues`. Processing units dynamically start and shut down based on `user load`, addressing `variable scalability`. `With no central database bottleneck, near-infinite scalability is achieved`.

Key components include processing units with application code, virtualized middleware for unit management, data pumps for asynchronous data updates to the database, data writers for database updates, and data readers delivering database data to processing units on startup.

??? example
    ![Space-based architecture basic topology from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/space-based-basic-topology.png)
    > Space-based architecture basic topology from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

### Processing Unit

The processing unit (as shown in the example image), `encompasses the application logic, both web-based components and backend business logic`. Its content varies depending on the application type. Smaller web-based apps might reside in a single processing unit, while larger ones may distribute functionality across multiple units based on application areas. The processing unit may also host small, single-purpose services (akin to microservices). `Alongside the application logic, it integrates an in-memory data grid and replication engine`, often implemented using products like Hazelcast, Apache Ignite, or Oracle Coherence.

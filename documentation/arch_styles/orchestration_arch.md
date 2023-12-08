# Orchestration-Driven Service-Oriented Architecture

!!! danger
    This architecture style `represents an era-specific architectural style` influenced by external forces and organizational philosophies. Despite its logical foundation, `this architecture faced challenges that ultimately led to its downfall. It serves as a notable example of how a seemingly rational organizational idea can impede crucial aspects of the development process`.

## History and Philosophy

In the late 1990s, the Orchestration-Driven Service-Oriented Architecture emerged as enterprises were rapidly expanding, necessitating sophisticated IT solutions. During this era, `companies faced challenges related to limited and expensive computing resources, prompting the adoption of distributed architectures for their scalability benefits`. The prevailing constraints were driven by factors such as the cost of operating systems and complex licensing schemes for commercial database servers.

`As a result, architects were compelled to maximize reuse`. The dominant philosophy underlying this architecture was centered on `achieving extensive reuse in all forms, with far-reaching consequences`.

## Topology

The topology varied among implementations, but the overarching concept involved `establishing a taxonomy of services within the architecture, with each layer assigned specific responsibilities`.

This style of architecture is inherently `distributed`, and the precise delineation of boundaries varied depending on the organization's specific requirements and structure.

!!! example
    ![Topology of orchestration-driven service-oriented architecture from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/orchestration-example.png)
    > Topology of orchestration-driven service-oriented architecture from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

## Taxonomy

`The services played a crucial role in this architecture centered around enterprise-level reuse`. Many large companies were annoyed at how much they had to continue to rewrite software. The various layers in this taxonomy were designed to support this objective.

### Business Servicess

Situated at the `top of the architecture`, business services `served as the entry point and encapsulated domain-specific behavior`. Examples like ExecuteTrade or PlaceOrder represented essential business activities. `These service definitions, often crafted by business users, contained input, output, and schema information but no actual code`.

### Enterprise Services

Found beneath business services, `enterprise services housed fine-grained, shared implementations`. `Development teams focused on creating atomic behavior around specific business domains, such as CreateCustomer or CalculateQuote`. `These services acted as the foundational building blocks for the broader business services, connected through an orchestration engine`. The goal was to foster reuse by developing finely tuned enterprise services that could be leveraged across various business workflows.

However, the `dynamic nature of the business landscape posed challenges to achieving complete stability`. Markets, technological advancements, and other factors complicated efforts to establish long-term stability in the software world.

### Application Services

`Recognizing that not all services required the same level of granularity or reuse, application services were introduced`. These were one-off, `single-implementation services tailored to specific application needs`. For instance, an application might need a geo-location service without the organization investing in making it reusable. Application services were typically owned by a single application team, addressing specific requirements without the expectation of broader reuse.

### Infrastructure Services

Handling operational concerns like `monitoring, logging, authentication, and authorization`, infrastructure services constituted the bottom layer. These services provided concrete implementations and were owned by a shared infrastructure team working closely with operations to ensure the smooth functioning of the overall system.

### Orchestration Engine

`At the heart of the Orchestration-Driven Service-Oriented Architecture lies the orchestration engine`. This pivotal component `intricately threads together the implementations of business services` through orchestration, encompassing features such as transactional coordination and message transformation.  In contrast to microservices architectures, where each service might maintain its database, `this architecture typically relies on a single relational database or a few databases`. As a result, `transactional behavior is declaratively managed within the orchestration engine rather than in individual databases`.

The orchestration engine plays a pivotal role in `defining the relationships between business and enterprise services`, determining their alignment, and establishing transaction boundaries. It also operates as an integration hub, facilitating the seamless integration of custom code with packaged and legacy software systems.

Being the central element of the architecture, `the team of integration architects responsible for the orchestration engine tends to emerge as a potent political force within the organization`, often evolving into a bureaucratic bottleneck, in line with Conway's law predictions.

While the notion of off-loading transaction behavior to an orchestration tool seemed promising, practical implementation proved to be challenging. `Determining the optimal granularity of transactions became increasingly intricate`. While constructing a few services encapsulated in a distributed transaction is feasible, `the architecture's complexity heightens as developers grapple with defining appropriate transaction boundaries between services`.

### Message Flow

In this architecture, all requests traverse the orchestration engine, serving as the locus of logic. Consequently, the message flow is directed through the engine even for internal calls.

!!! example
    The `CreateQuote` business-level service initiates a call to the service bus, defining the workflow involving calls to `CreateCustomer` and `CalculateQuote`. Each of these, in turn, encompasses calls to application services. The service bus acts as the intermediary for all calls, functioning both as an integration hub and an orchestration engine.

    ![Message flow with service-oriented architecture from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/orchestration-example-message.png)
    > Message flow with service-oriented architecture from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

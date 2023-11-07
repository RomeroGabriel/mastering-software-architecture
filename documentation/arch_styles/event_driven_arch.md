# Event-Driven Architecture Style

The event-driven architecture style is a well-liked method for `building applications that need to be both highly scalable and high-performing`. It's quite flexible and can be `used for both small and large applications`, making it a popular choice across the board. This style involves `components that process events independently, without being tightly connected`. `It can be its own architecture style or be part of other styles`, like event-driven microservices architecture.

In many applications, there's a `request-based approach, where a central system manages and directs various requests to the right places`. This can be a user interface, an API layer, or an enterprise service bus. `These places handle the requests, dealing with tasks like retrieving or updating data in a database`.

![Request-based model from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/event-driven-model.png)
> Request-based model from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

??? example "Request-Based Example"
    For instance, when a customer requests their order history for the past six months, `it involves retrieving data within a specific context, making it a data-driven, deterministic request`. This aligns with the request-based model.

`An event-based model responds to specific situations, triggering actions based on those events`.

!!! example "Event-Based Model Example"
    For example, in an online auction, submitting a bid isn't a direct request to the system but `an event that occurs after the current asking price is announced`. `The system must react to this event by comparing the bid to others received simultaneously, determining the current highest bidder`.

## Topology

`Two main topologies are prevalent in event-driven architecture: the mediator topology and the broker topology`. Understanding the distinct characteristics and implementation strategies of these topologies is crucial to determining the most suitable choice for a given situation.

!!! info "The Mediator Topology"
    The mediator topology is commonly applied when you need to manage the workflow of an event process.

!!! info "The Broker Topology"
    The broker topology is favored when you need swift responsiveness and dynamic control over event processing.

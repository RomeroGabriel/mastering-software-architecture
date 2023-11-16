# Event-Driven Architecture Style

The event-driven architecture style is a well-liked method for `building applications that need to be both highly scalable and high-performing`. It's quite flexible and can be `used for both small and large applications`, making it a popular choice across the board. This style involves `components that process events independently, without being tightly connected`. `It can be its own architecture style or be part of other styles`, like event-driven microservices architecture.

In many applications, there's a `request-based approach, where a central system manages and directs various requests to the right places`. This can be a user interface, an API layer, or an enterprise service bus. `These places handle the requests, dealing with tasks like retrieving or updating data in a database`.

![Request-based model from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/event-driven-model.png)
> Request-based model from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

??? example "Request-Based Example"
    For instance, when a customer requests their order history for the past six months, `it involves retrieving data within a specific context, making it a data-driven, deterministic request`. This aligns with the request-based model.

`An event-based model responds to specific situations, triggering actions based on those events`.

??? example "Event-Based Model Example"
    For example, in an online auction, submitting a bid isn't a direct request to the system but `an event that occurs after the current asking price is announced`. `The system must react to this event by comparing the bid to others received simultaneously, determining the current highest bidder`.

## Topology

`Two main topologies are prevalent in event-driven architecture: the mediator topology and the broker topology`. Understanding the distinct characteristics and implementation strategies of these topologies is crucial to determining the most suitable choice for a given situation.

!!! info "The Mediator Topology"
    The mediator topology is commonly applied when you need to manage the workflow of an event process.

!!! info "The Broker Topology"
    The broker topology is favored when you need swift responsiveness and dynamic control over event processing.

### Broker Topology

The broker topology in event-driven architecture `differs from the mediator topology by not having a central event mediator`. Instead, the `message flow is spread across the event processor components in a chain-like broadcasting style through a lightweight message broker`. This topology is `beneficial for relatively straightforward event processing flows` where central event orchestration and coordination are unnecessary.

There are four main parts in the broker topology: `an initiating event, the event broker, an event processor, and a processing event`.

!!! note "Initiating Event"
    This is the starting point of the entire event flow.

!!! note "Event Broker"
    The initiating event is sent to an event channel in the event broker for processing.

!!! note "Event Processor"
    Since there is no mediator component, a single event processor receives the initiating event from the event broker and begins the processing of that event. The event processor executes a specific task related to the event and asynchronously broadcasts its actions to the entire system, creating a processing event.

!!! note "Processing Event"
    This processing event is then sent to the event broker for further processing, if necessary. Other event processors, upon listening to the processing event, react to it by performing actions and then advertise, through a new processing event, what they did. This process continues until no one is interested in the actions of a final event processor.

In the broker topology, it is considered `good practice for each event processor to advertise its actions to the entire system`, even if other event processors may not be concerned. This practice `ensures architectural extensibility in case additional functionality is required for processing that event`.

!!! example "Email Notifying"
    Suppose an email needs to be generated and sent to a customer to inform them about a specific action.
    1. The `Notification event processor` generates and dispatches the email.
    1. It then `advertises this action to the entire system by creating a new processing event`, sending it to a topic.
    1. However, since no other event processors are tuned in to events on that topic, the message `simply fades away without any further impact`.

Here's a notable illustration of `architectural extensibility`. `Although it might appear inefficient to send messages that go unnoticed, it holds significant value`. Consider a scenario where a new requirement emerges to analyze emails sent to customers. With the current system:

1. A new `event processor for analyzing emails can seamlessly be introduced` with minimal effort.
1. The email information is readily accessible via the email topic, allowing the new analyzer to function without the need for additional infrastructure or changes to other event processors.

!!! example "More Deep Example"
    ![Example of the broker topology [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/event-driven-model-example.png)
    > Example of the broker topology [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

    1. The `initial event` is "Purchasing Book."
    1. The `event broker` is represented by the `[PlaceOrder]` pipe.
    1. `Event processors` are depicted as boxes, like `OrderPlacement`, `Payment`, `Notification`, etc.
    1. `Processing events`  are illustrated by pipes with arrows and names in lowercase, like `[order-created]`, `[inventory-updates]`, `[payment-denied]`, etc.

It's evident that `all event processors are highly decoupled and operate independently`. `Once an event processor hands off the event, it ends involvement in the processing of that specific event, remaining available to react to other initiating or processing events`. Moreover, `each event processor can scale independently` to handle varying load conditions or backups in the event processing.

While the broker topology offers benefits in terms of performance, responsiveness, and scalability, there are `drawbacks`. Firstly, `there is no control over the overall workflow associated with the initiating event`. The system lacks awareness of when the business transaction of placing an order is truly complete. `Error handling poses a significant challenge in the broker topology`. Without a mediator monitoring or controlling the business transaction, a failure goes unnoticed, leading to a stuck business process that requires automated or manual intervention to resolve.

`Recovering from a business transaction (recoverability) is not supported in the broker topology`. As other actions are asynchronously taken during the initial processing of the initiating event, resubmitting the initiating event becomes impractical. `No component in the broker topology is aware of or owns the state of the original business request, leaving no one responsible for restarting the business transaction and knowing its progress`.

| Advantages      | Disadvantages                          |
| ----------- | ------------------------------------ |
| `Highly decoupled event processors`       | Workflow control  |
| `High scalability`       | Error handling |
| `High responsiveness`    | Recoverability |
| `High performance`    | Restart capabilities |
| `High fault tolerance`    | Data inconsistency |

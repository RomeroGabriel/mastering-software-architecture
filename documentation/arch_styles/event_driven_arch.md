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

| Advantages  | Disadvantages |
| ----------- | ------------------------------------ |
| `Highly decoupled event processors`       | Workflow control  |
| `High scalability`       | Error handling |
| `High responsiveness`    | Recoverability |
| `High performance`    | Restart capabilities |
| `High fault tolerance`    | Data inconsistency |

### Mediator Topology

In the mediator topology, a central figure is the `event mediator, overseeing and orchestrating the workflow for initiating events that necessitate the coordination of multiple event processors`. The key components of the mediator topology include an initiating event, an event queue, an event mediator, event channels, and event processors.

!!! note "Initiating Event"
    1. This is the event that initiates the entire eventing process.
    1. `The initiating event is directed to an initiating event queue, which is then received by the event mediator`.

!!! note "Event Mediator"
    1. Manages the workflow, generating corresponding processing events dispatched to dedicated event channels (usually queues) in a point-to-point messaging style.

!!! note "Event Processors"
    1. Attend to their tasks by `monitoring dedicated event channels, executing event-specific processes, and typically communicating back to the mediator upon task completion`.
    1. Unlike the broadcast approach of the broker topology, `event processors in the mediator setup operate discreetly without announcing their actions to the entire system`.

Practical implementations often `deploy multiple mediators, each linked to a specific domain or category of events`. This strategic approach `mitigates the risk of a single point of failure`, enhancing overall system resilience and performance.

The mediator component, distinctive from the broker topology, `boasts both knowledge and command over the workflow`. This capability empowers the mediator to uphold event states and proficiently manage aspects like error handling, recoverability, and restart functionalities.

A fundamental disparity surfaces between the processing events in broker and mediator topologies concerning their meaning and utilization. In the `broker paradigm, processing events serve as published occurrences in the system` (e.g., order-created, payment-applied, email-sent), `triggering subsequent actions and reactions among event processors`. Using the `mediator topology, processing events` (e.g., place-order, send-email, fulfill-order) `are akin to commands, dictating necessary actions rather than merely reporting past events`. Notably, in the `mediator domain, a command necessitates processing, while an event in the broker setup can be disregarded`.

!!! warning "Challenges within the Mediator Domain"
    Although event processors can scale comparably to the broker setup, the `mediator's scaling introduces occasional bottlenecks` in the overarching event processing flow. Additionally, `event processors in the mediator setup lack the high level of independence` seen in the broker model, impacting overall performance due to the mediator's active role in controlling event processing.

| Advantages  | Disadvantages |
| ----------- | --------------|
| `Workflow control` | More coupling of event processors |
| `Error handling` | Lower scalability |
| `Recoverability` | Lower performance |
| `Restart capabilities` | Lower fault tolerance |
| `Better data consistency` | Modeling complex workflows |

## Asynchronous Capabilities

The event-driven architecture style presents a distinctive feature compared to other architectural approaches by `relying entirely on asynchronous communication`. This encompasses both `fire-and-forget processing`, where no response is required, and `request/reply` processing, where a response is expected from the event consumer. Leveraging asynchronous communication proves to be a `potent technique for enhancing overall system responsiveness`.

### Responsiveness vs Performance

In scenarios where the `user doesn't necessitate immediate feedback` beyond an acknowledgment or a simple thank-you message, why subject them to unnecessary waiting? `Responsiveness focuses on promptly notifying the user that their action has been acknowledged and will undergo processing shortly`. Conversely, `performance revolves around expediting the end-to-end process`.

`The challenge in asynchronous behavior arises when the user's action encounters rejection`, as there's no direct route to communicate this back to the end user. While a message signaling an issue could be dispatched, in more intricate scenarios, this might not constitute a comprehensive solution. The primary hurdle in asynchronous communications lies in error handling. `Although responsiveness sees a significant boost, effectively addressing error conditions adds complexity to the event-driven system`.

## Error Handling

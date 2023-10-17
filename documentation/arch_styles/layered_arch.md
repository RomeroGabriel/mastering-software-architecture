# Layered Architecture Style

Layered architecture, or the `n-tiered architecture style`, is a widely used and popular architecture style in software development. Its popularity stems from its `simplicity, familiarity, and cost-effectiveness`. In most organizations, there are user interface (UI) developers, backend developers, rules developers, and database experts (DBAs). `This style seamlessly accommodates various roles in an organization`, making it a natural choice for many business applications. This architecture style is particularly `well-suited for applications that require a clear separation of concerns and modularity`. It allows for the division of an application into distinct layers, with each layer responsible for specific functions. Typically, these layers include:

!!! info "Presentation Layer (UI)"
    This is the user interface layer responsible for handling user interactions. It often includes web pages or user interfaces in desktop applications.

!!! info "Business Logic Layer"
    Also known as the application layer, this layer contains the core logic and business rules of the application. It processes requests from the presentation layer and communicates with the data access layer.

!!! info "Data Access Layer"
    This layer is responsible for interacting with the database or data storage. It performs tasks such as data retrieval, storage, and manipulation.

!!! info "Database Layer"
    This layer involves the actual database system where data is stored and managed.

However, it is important to note that the layered architecture style is associated with certain `architectural anti-patterns`, such as the `architecture by implication anti-pattern` and the `accidental architecture anti-pattern`. These issues can arise when the development process `lacks proper planning or when the architecture is not explicitly defined`.

In practical terms, `if developers or architects are uncertain about the architecture style` being employed, or if an Agile development team initiates coding without a clear architectural plan, `it is highly probable that they are adopting the layered architecture style`.

## Topology

The layered architecture style `organizes components into distinct horizontal layers, each with a specific function within the application`. While the `number and types of layers can vary`, the typical layered architecture comprises four fundamental layers: presentation, business, persistence, and database. `Each layer assumes a defined role and responsibility, abstracting the necessary tasks to fulfill specific business requests`.

!!! example
    For instance, the `presentation layer focuses on displaying information in a specific format, without requiring knowledge about data retrieval processes`. This segregation of concerns allows for the `establishment of clear role and responsibility models within the architecture`. Components within a particular layer are confined to tasks pertinent to that layer, ensuring a focused and modular approach to development.

However, this structured separation in the layered architecture `can potentially lead to a decrease in overall agility, hampering the ability to swiftly adapt to changes`. As a technically partitioned architecture, i`t groups components by their technical roles rather than by business domains`. Consequently, a `specific business domain`, like "customer," `spans various layers within the architecture, making it challenging to implement changes within that domain`. This characteristic makes it less suitable for the effective implementation of a domain-driven design approach.

### Deployment

The `deployment of the layered architecture style can take several physical layering forms, resulting in distinct topology variants.`

!!! note "The First Variant"
    The `presentation, business, and persistence layers into a singular deployment unit`. Simultaneously, the database layer remains external, often as a distinct physical database or filesystem.

!!! note "The Second Variant"
    The `presentation layer is physically separated into its deployment unit`, while the `business and persistence layers are combined into a second deployment unit`. As in the first variant, the `database layer is typically segregated into an external database or filesystem`.

!!! note "The Third Variant"
    The third variant amalgamates `all four standard layers, including the database layer, into a single deployment unit`. This approach proves beneficial for smaller applications, especially those utilizing either an internally embedded database or an in-memory database.

`The choice of a deployment variant should align with the specific requirements of the application`, including considerations related to application size, performance demands, and the necessity for scalability and flexibility.

## Layers

### Layers of Isolation

In the `context of the layered architecture style, layers can be classified as either closed or open`.

!!! info "Closed Layers"
    A closed layer mandates that a request `must pass through each layer in a sequential top-down manner`, without the ability to skip any intermediary layers.

!!! info "Open Layers"
    In contrast with Closed Layers, an `open layer allows a request to bypass other layers`, potentially leading to a more flexible but complex system.

Determining whether open or closed layers are preferable depends on the concept of `layers of isolation`. This concept `emphasizes that modifications in one layer typically do not affect components in other layers`, provided that the contracts between the layers remain unchanged. This independence among layers minimizes the interdependencies between them, facilitating maintainability and adaptability.

However, `to ensure effective layers of isolation, layers involved in the primary flow of requests should be closed`. Allowing direct access from the presentation layer to the persistence layer, for instance, can tightly couple the application's components, making the architecture rigid and difficult to modify.

The layers of isolation concept also `enable seamless layer replacements without impacting other layers, assuming well-defined contracts` and the utilization of appropriate design patterns. Leveraging this concept in the layered architecture style enables the replacement of outdated components, such as migrating from JavaServer Faces (JSF) to React.js for the presentation layer, without necessitating changes in other parts of the application.

### Adding Layers

While closed layers promote effective isolation and encapsulation of change within the architecture, `there are instances where incorporating open layers can be advantageous`. For instance, a layer with `common functionalities` like date and string utility classes, logging classes, and similar utilities might benefit from being an `open layer`. `This approach facilitates convenient accessibility across various parts of the architecture`.

`The concept of open and closed layers plays a critical role in defining the relationship between architecture layers and the flow of requests`. It offers developers essential insights into the access restrictions of different layers within the architecture. `Properly documenting and communicating the status of open and closed layers`, along with the rationale behind these decisions, `is crucial`. Neglecting to provide clear documentation or communication about the openness or closedness of layers can result in tightly coupled and fragile architectures that are challenging to test, maintain, and deploy.

`By strategically incorporating open layers to accommodate common functionalities and by clearly delineating the access restrictions within the architecture`, developers can create a more `flexible and adaptable system while maintaining the benefits of layered isolation`.

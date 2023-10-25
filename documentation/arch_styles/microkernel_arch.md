# Microkernel Architecture Style

The concept of the microkernel architecture, often termed the `plug-in architecture`, originated many years ago and `continues to be a prominent feature in modern software design`. This style particularly `suits product-based applications`, which are typically distributed as a single, comprehensive deployment, `installed at the customer's location as a third-party product`. Its utility isn't limited to products, as it also finds extensive use in custom-built business applications.

## Topology

Microkernel architecture is a `basic two-components monolithic structure`. It consists of a `core system and plug-in components`. This setup divides the `application logic between the autonomous plug-ins` and the `fundamental core system`, allowing for flexibility, customization, and segregation of application features and specific processing logic.

![Basic components of the microkernel architecture style from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microkernel_arch_example.png)
> Basic components of the microkernel architecture style from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

The `core system assumes the responsibility of supplying necessary data to each plug-in`. Decoupling is the main rationale behind this strategy. `Any modifications to the database should only affect the core system`, not the plug-in components. However, `plug-ins can maintain their own distinct data stores accessible solely to their respective plug-ins`.

![Plug-in components can own their own data store from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microkernel_dbs.png)
> Plug-in components can own their own data store from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

### Core System

`The core system is the essential functionality needed to operate the system`. For instance, `an IDE it's the basic text editor` enabling actions like opening, editing, and saving files. It's `only when plug-ins are added that it becomes a fully functional product`.

Another definition of the core system is the `straightforward path through the application`, without custom processing. `Transferring complex functions to plug-ins simplifies the core system, making it more extensible, maintainable, and testable`.

Depending on the application's scale, the `core system can be structured as a layered architecture or a modular monolith`. Additionally, it can be split into separately deployed domain services, each containing domain-specific plug-in components.

??? example
    ![Variations of the microkernel architecture core system from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/core-example-1.png)
    > Variations of the microkernel architecture core system from [Fundamentals of  Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

    ![User interface variants from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/core-example-1.png)
    > User interface variants from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

### Plug-In Components

`Plug-in components are self-contained units housing specific functionalities, additional features, and customized code designed to amplify or extend the core system`. They also serve to `isolate volatile code`, enhancing the application's maintainability and testability. `The goal is to ensure plug-in components remain independent without interdependencies`.

These plug-in components can be either `compile-based or runtime-based`. `Runtime plug-ins can be added or removed without redeploying the core system or other plug-ins`. In contrast, `compile-based` plug-ins are more straightforward to manage but necessitate `redeployment of the entire monolithic application when modified, added, or removed`.

`Communication between the plug-in components and the core system typically occurs through point-to-point connections`. This connection, often represented as a `pipe`, is generally a method invocation or function call to the entry-point class of the plug-in component. While plug-in components `primarily engage in point-to-point communication` with the core system, `there are alternatives such as using REST or messaging to invoke plug-in functionality`.

In this scenario, `each plug-in functions as a standalone service`, or even a microservice implemented within a container. Although this approach may seem conducive to scalability, it's important to note that this setup `remains a single architecture quantum due to the monolithic core system. Consequently, every request must first pass through the core system to access the plug-in service`.

??? example
    ![Remote plug-in access using REST from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microkernel-rest.png)
    > Remote plug-in access using REST from [Fundamentals of  Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

### Trade-Offs

`Enabling remote plug-in access transforms the microkernel architecture into a distributed one`, which can pose challenges for implementing and deploying most third-party on-prem products. Additionally, it introduces increased complexity, higher costs, and complicates the overall deployment structure.

`Deciding whether to establish communication to plug-in components from the core system as point-to-point or remote should be based on specific requirements`, necessitating a thorough analysis of the trade-offs between the benefits and drawbacks of each approach.

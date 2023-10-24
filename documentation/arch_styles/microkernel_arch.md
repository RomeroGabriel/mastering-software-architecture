# Microkernel Architecture Style

The concept of the microkernel architecture, often termed the `plug-in architecture`, originated many years ago and `continues to be a prominent feature in modern software design`. This style particularly `suits product-based applications`, which are typically distributed as a single, comprehensive deployment, `installed at the customer's location as a third-party product`. Its utility isn't limited to products, as it also finds extensive use in custom-built business applications.

## Topology

Microkernel architecture is a `basic two-components monolithic structure`. It consists of a `core system and plug-in components`. This setup divides the `application logic between the autonomous plug-ins` and the `fundamental core system`, allowing for flexibility, customization, and segregation of application features and specific processing logic.

![Basic components of the microkernel architecture style from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/microkernel_arch_example.png)
> Basic components of the microkernel architecture style from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

## Core System

`The core system is the essential functionality needed to operate the system`. For instance, `an IDE it's the basic text editor` enabling actions like opening, editing, and saving files. It's `only when plug-ins are added that it becomes a fully functional product`.

Another definition of the core system is the `straightforward path through the application`, without custom processing. `Transferring complex functions to plug-ins simplifies the core system, making it more extensible, maintainable, and testable`.

Depending on the application's scale, the `core system can be structured as a layered architecture or a modular monolith`. Additionally, it can be split into separately deployed domain services, each containing domain-specific plug-in components.

??? example
    ![Variations of the microkernel architecture core system from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/core-example-1.png)
    > Variations of the microkernel architecture core system from [Fundamentals of  Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

    ![User interface variants from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/arch_styles/core-example-1.png)
    > User interface variants from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

## Plug-In Components

# Components

Modules are groups of related code, but architects often focus on `components, which are the physical versions of modules`. These components are packaged differently depending on the programming language, such as jar files in Java or DLLs in .NET.

## Component Scope

Components provide a language-specific way to group artifacts together, often by nesting them to create layers. It's helpful to divide the concept of components as shown in the image below.

![Different varieties of components](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/components/component_scope.png)
> *Different varieties of components*

??? info "Wrapper of Related Code"
    The simplest form of a component is one that `wraps code at a higher level of modularity than classes or functions`. This is often `referred to as a library`. Libraries typically run in the same memory address as the calling code and communicate via language function call mechanisms. Libraries are usually compile-time dependencies.

??? info "Layer or Subsystem & Event Processor"
    Components can also take the form of subsystems or layers within an architecture, serving as the deployable units of work for many event processors.

??? info "Distributed Service"
    Distributed services tend to `run in their own separate address spaces and communicate` using low-level networking protocols like TCP/IP or higher-level formats like REST or message queues. `They are stand-alone and deployable units in architectures` such as microservices.

`Components are the basic building blocks in architecture` and are a crucial consideration for architects. `One of the key decisions architects must make is how to divide the architecture into top-level components`. While architects are not obligated to use components, they often find them beneficial as they provide a higher level of modularity.

## Architect Role

`The architect typically plays a central role in defining, refining, managing, and overseeing components within an architecture`.  This work is done in collaboration with various stakeholders, including business analysts, subject matter experts, developers, QA engineers, operations teams, and enterprise architects, to create the initial software design.

In most cases, components represent the lowest level of the software system that an architect directly interacts with. These components are composed of classes or functions, depending on the implementation platform. The detailed design of these classes or functions often falls under the responsibility of tech leads or developers. While `architects may involve themselves in class design, especially when applying design patterns, they should avoid micromanaging every decision throughout the system`. Allowing other roles to make significant decisions is essential for empowering the next generation of architects.

`One of the architect's initial tasks on a new project is to identify components`. However, before doing so, architects must have a clear understanding of how to partition the overall architecture effectively.

## Architecture Partitioning

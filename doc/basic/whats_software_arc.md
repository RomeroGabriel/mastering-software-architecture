
# What is Software Architecture?

Software Architecture is a **dynamic and complex** field that **continues to evolve rapidly**. Recent years have witnessed advancements such as CI/CD, microservices, containerization, and cloud-based resources. These innovations bring new capabilities and trade-offs to consider.

In software development, understanding **trade-off analysis is crucial** for making informed decisions. This repository emphasizes analyzing trade-offs rather than passing judgments on technologies.

It is crucial to recognize that **architectures are shaped by their context**. Architectural decisions are often **influenced by the realities of the environment** they operate in. For instance, attempting to implement a microservices architecture in 2002 would have been impractical.

## Defining Software Architecture

Defining Software Architecture is challenging due to various interpretations. It may be seen as the blueprint or roadmap for a system. However, what aspects does an architect analyze when examining an architecture?

One definition in [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/) is illustrated on the image bellow. In this definition, software architecture consists of the **structure** of the system, combined with **architecture characteristics** the system must support, **architecture decisions**, and **design principles**.

![Architecture consists of the structure combined with architecture characteristics (“-ilities”), architecture decisions, and design principles](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/basic/arch_definition.png)
> *Architecture consists of the structure combined with architecture characteristics (“-ilities”), architecture decisions, and design principles*

### Structure

![Structure refers to the type of architecture styles used in the system](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/basic/arch_structure.png)
> *Structure refers to the type of architecture styles used in the system*

The system **structure** refers to the **architecture style**(s) implemented in the system, like microservices, layered, or microkernel. However, it's important to note that the system structure alone does not fully describe a system architecture.

### Architecture characteristics

![Architecture characteristics refers to the “-ilities” that the system must support](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/basic/arch_charac.png)
> *Architecture characteristics refers to the “-ilities” that the system must support*

Architecture characteristics **define the success criteria** for a system, independent of its functionality. They are essential for the system to function correctly and **do not necessarily rely on knowing the specifics of its functionality**.

### Architecture decisions

![Architecture decisions are rules for constructing systems](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/basic/arch_decision.png)
> *Architecture decisions are rules for constructing systems*

Architecture decisions establish the **guidelines for system construction**. They impose constraints and provide direction to development teams, outlining **what is permissible and what is not within the system**.

### Design principles

![Design principles are guidelines for constructing systems](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/doc/images/basic/arch_principle.png)
> *Design principles are guidelines for constructing systems*

The design principles is a **guideline** rather than a hard-and-fast rule like architecture decisions.
As an example, the design principle depicted in the image above **guides development team** to utilize asynchronous messaging for improved performance in a microservice architecture. **Architecture decisions cannot account for every communication scenario between services**. Hence, design principles offer guidance, such as employing async messaging, enabling developers to choose suitable communication protocols like REST or gRPC.

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

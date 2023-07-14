# Architectural Thinking

A software architecture goes beyond mere "thinking about the architecture." It encompasses various crucial aspects that architects need to consider, including:

- Architecture vs. Design: It is important to *distinguish between architecture and design* and effectively collaborate with development teams to align their efforts.

- Technical Breadth: It involves having a broad range of technical knowledge while *maintaining a certain level of depth*. This allows architects to see solutions and possibilities that others do not see.

- Analyzing Trade-Offs: Architects should *understand, analyze, and reconcile trade-offs between different solutions and technologies*.

- Understanding Business Drivers: Understand the importance of business drivers and how they translate to architectural concerns.

## Architecture vs. Design

The distinction between architecture and design can be confusing at times. It raises questions about the roles and responsibilities of architects compared to developers. However, an **architect possesses the knowledge and understanding to differentiate between architecture and design**. They recognize how these two aspects intricately intertwine to create comprehensive solutions for both business and technical challenges.

### Traditional and Wrong Thinking

![Traditional view of architecture versus design from Fundamentals of Software Architecture book](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/basic/arch_design_wrong.png)
> Traditional view of architecture versus design from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

The traditional viewpoint described in the image below is rarely effective. It often leads to a **disconnect between the architect and the development team**. Architectural decisions made by the architect may not reach the development team, and conversely, decisions made by the development team may not be communicated back to the architect. This *lack of communication* and coordination can result in **changes to the architecture that were never intended or considered by the architect**.

### The Right Thinking

![Making architecture work through collaboration from Fundamentals of Software Architecture book](https://raw.githubusercontent.com/RomeroGabriel/mastering-software-architecture/main/documentation/images/basic/arch_design_right.png)
> Making architecture work through collaboration from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

For effective architecture, there should be **no barriers between architects and developers**. It is crucial to establish a strong, *bi-directional relationship between them*. This allows architects to provide mentoring and coaching to the development team. **Architecture and design are intertwined aspects within the software project lifecycle and must always collaborate closely.**

## Technical Breadth

A significant aspect of an architect's value lies in their comprehensive **understanding of technology and its application to solving specific problems**. Rather than having expertise in only one solution, it is more advantageous for an architect **to be aware of multiple solutions available** for a given problem.

In the realm of architecture, *breadth of knowledge outweighs depth*. Architects are tasked with **making decisions that align capabilities with technical constraints**. Therefore, having a broad understanding of a wide range of solutions holds immense value.

## Analyzing Trade-Offs

> Architecture is the stuff you can’t Google.
> There are no right or wrong answers in architecture—only trade-offs.
> Programmers know the benefits of everything and the trade-offs of nothing. Architects need to understand both.

Adopting an architectural mindset involves **recognizing trade-offs in every solution**, whether they are technical or non-technical, and meticulously analyzing them to **determine the optimal choice**.

In architecture, trade-offs permeate every aspect, which is why the universal response to architecture questions is often "it depends." The optimal solution hinges on various factors such as the deployment environment, business drivers, company culture, budgets, timeframes, developer skill sets, and numerous other considerations.

As an architect, the ability to navigate these trade-offs is *crucial*. It entails carefully **evaluating the benefits and drawbacks of different options and striking a balance that aligns with the specific project requirements and constraints**. Making informed decisions based on a thorough analysis of trade-offs ensures the chosen solution is well-suited to the unique context of the architecture project.

## Understanding Business Drivers

Thinking like an architect entails comprehending the essential business drivers necessary for the system's success and **effectively translating those requirements into architectural characteristics** like scalability, performance, and availability. This task presents a significant challenge, as it demands architects to possess a certain level of business domain knowledge and foster collaborative relationships with key business stakeholders. By understanding the underlying business needs and aligning them with the architectural decisions, architects can design solutions that meet both technical and business objectives, ensuring the overall success of the system.

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

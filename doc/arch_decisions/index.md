# Architecture Decisions

Architects play a pivotal role in making crucial architecture decisions that shape the application or system. `While these decisions primarily influence the structure of the application or system, they might also extend to technology choices, especially when they impact essential architectural characteristics`. Regardless of the context, a good architecture decision serves as a guiding force for development teams, helping them in making in making the right technical choices. The process involves `gathering relevant information, providing clear justifications, documenting decisions, and ensuring effective communication with the pertinent stakeholders`.

## Architecture Decision Anti-Patterns

Not surprisingly, `several pitfalls emerge when architects make decisions`. Three major architecture anti-patterns that often unfold during decision-making are the `Covering Your Assets` anti-pattern, the `Groundhog Day` anti-pattern, and the `Email-Driven Architecture` anti-pattern. These typically follow a progression: `overcoming the first leads to the second, and overcoming the second leads to the third`. Navigating architecture decisions successfully requires architects to address each of these anti-patterns.

!!! note "1. Covering Your Assets Anti-Pattern"
    `This occurs when architects avoid or delay decisions due to the fear of making the wrong choice`. To overcome this anti-pattern, `architects can either wait until the last responsible moment to decide or collaborate continually with development teams to ensure the decision aligns with implementation realities`.

    `Waiting until the last responsible moment means gathering enough information to justify and validate the decision without causing delays or succumbing to analysis paralysis`. Collaborating with development teams is crucial because architects can't possibly anticipate every detail about a technology. `Close collaboration enables swift adjustments to the decision if issues arise`.

    For instance, if an architect decides to cache product-related reference data in all service instances using a read-only replicated cache, collaboration with development teams may reveal scalability issues that prompt a revision of the decision.

!!! note "2. Groundhog Day Anti-Pattern"
    Once architects overcome the first anti-pattern, they may encounter the Groundhog Day anti-pattern. `This unfolds when people repeatedly discuss a decision without a clear understanding of why it was made`.

    The Groundhog Day anti-pattern `arises when architects fail to provide a comprehensive justification for their decisions`. When justifying architecture decisions, `it's crucial to offer both technical and business justifications`.
    
    For instance, a decision to break apart a monolithic application into separate services `should not only highlight technical benefits but also articulate the business value, such as faster delivery of new functionality or cost reduction`. Providing business value is a litmus test for determining the validity of an architecture decision. If a decision lacks business value, it might not be a sound one and should be reconsidered.

!!! note "3. Email-Driven Architecture Anti-Pattern"
    Once architects make decisions and fully justify them, a third architecture anti-pattern emerges: Email-Driven Architecture. `This anti-pattern occurs when people are unaware of an architecture decision, leading to implementation challenges`.

    `Effectively communicating architecture decisions is crucial to avoid the Email-Driven Architecture anti-pattern`. Rather than including the decision in the body of an email, `architects should provide a link to a single system of record for the decision, whether it's a wiki page or a document`. This ensures a centralized and accessible repository for the decision and its details. Moreover, `notifying only relevant stakeholders further enhances communication effectiveness, preventing information overload`.

By addressing these anti-patterns, architects can enhance the decision-making process, fostering clarity, collaboration, and successful implementation.

## Architecturally Significant

There exists a common misconception among architects that decisions involving specific technologies are merely technical choices rather than architecture decisions. However, this isn't always the case. `If an architect decides to adopt a particular technology because it directly supports a specific architecture characteristic, such as performance or scalability, then it qualifies as an architecture decision`.

The concept of `Architecturally Significant helps delineate which decisions fall under the architect's purview`. `These decisions notably impact the patterns or styles of architecture in use`. For instance, choosing to share data among a set of microservices is an architecturally significant decision. This choice influences the bounded context of each microservice, thereby affecting the overall structure of the application.

`Dependencies`, another aspect, `revolve around coupling points between components or services within the system`. These dependencies have far-reaching effects on scalability, modularity, agility, testability, reliability, and more.

`Interfaces` represent `how services and components are accessed and orchestrated`, typically through gateways, integration hubs, service buses, or API proxies. `Decisions related to interfaces involve defining contracts, including strategies for versioning and deprecation`. Due to their impact on users within the system, `interfaces are considered architecturally significant`.

Lastly, `construction techniques` encompass decisions about `platforms, frameworks, tools, and even processes`. While these decisions may seem technical, `they can have ramifications for various aspects of the architecture`.

`Understanding what constitutes an architecturally significant decision allows architects to focus on the key elements that shape the overall structure, dependencies, interfaces, and construction techniques of a system`. This clarity ensures that architects effectively contribute to the architectural integrity and success of the project.

## Architecture Decision Records

Effectively documenting architecture decisions is crucial for `maintaining clarity and coherence in a project`. [Architecture Decision Records (ADRs)](https://adr.github.io/) provide a structured way to capture and communicate these decisions. ADRs is a concise document typically spanning `one to two pages` that outlines a particular architectural decision. Although ADRs can be composed in `plain text`, they are commonly crafted using text document formats like `AsciiDoc`, `Markdown`, `wiki page template`. Additionally, specialized tools such as [ADR-tools](https://github.com/npryce/adr-tools) exist to facilitate the management of Architecture Decision Records

### Basic Structure

The basic structure of an ADR consists of five main sections: `Title`, `Status`, `Context`, `Decision`, and `Consequences`. Two more sections can be added: `Compliance` and `Notes`. This basic template is flexible enough to `include any other sections that may be deemed necessary`.

!!! note "Title"
    A concise, `numbered description` of the architecture decision, `providing clarity without ambiguity`.

!!! note "Status"
    Clearly define the status as `Proposed`, `Accepted`, or `Superseded`. Proposed decisions may require approval, and `Superseded decisions should reference the decision that replaces them`.

!!! note "Context"
    `Describe the driving forces behind the decision`, outlining the `specific situation` and `possible alternatives`. This section provides context for the decision-making process.

!!! note "Decision"
    Clearly articulate the decision along with its `justification`. Emphasize the `why` behind the decision rather than the `how`.

!!! note "Consequences"
    Detail the `impact of the decision`, `considering both positive and negative consequences`. Include `trade-off` analysis to weigh the impacts against the benefits.

!!! note "Compliance"
    Address how compliance with the decision will be `ensured`. `Specify whether compliance checks are manual or automated using fitness functions`. If automated, provide details on how fitness functions will be written and implemented.

!!! note "Notes"
    Include `metadata` such as the author's name and any additional relevant information.

### Storing ADRs

Once an architect creates an ADR, it must be `stored` somewhere. Regardless of where ADRs are stored, `each architecture decision should have its own file or wiki page`.

Some architects like to keep ADRs in the `Git repository` with the source code. Keeping ADRs in a Git repository `allows the ADR to be versioned and tracked as well`. However, for larger organizations, caution `against` this practice for several reasons. Firstly, `not everyone who needs to see the architecture decision may have access to the Git repository`. Secondly, the Git repository may not be a suitable place for storing ADRs that have a `context outside of the application Git repository`. This applies to integration architecture decisions, enterprise architecture decisions, or those decisions common to every application.

For these reasons, is recommend storing ADRs either in a `wiki`, using a wiki template, or in a `shared directory on a shared file server`. This ensures accessibility for all stakeholders through a wiki or other document rendering software.

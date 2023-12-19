# Choosing the Appropriate Architecture Style

`Determining the right architecture style can be a bit tricky`. With numerous choices available (and new ones popping up almost every day), `it's not that straightforward`. Choosing the appropriate architectural style `involves considering various factors within an organization and the specific software it's developing`. This decision-making process requires a careful `evaluation of trade-offs related to architectural characteristics, domain considerations, strategic goals, and several other variables`.

Even though the decision is deeply contextual, there are a few `pieces of general advice` that might come in handy as you navigate the landscape of architectural styles.

## Shifting “Fashion” in Architecture

`Understanding the dynamic landscape of architecture trends is crucial for architects`, regardless of where an organization currently stands in terms of architectural preferences. The ever-changing nature of preferred architecture styles is influenced by various factors:

??? note "Observations from the past"
    `New architecture styles often emerge from lessons learned and challenges faced in previous projects`. Architects draw from their past experiences to shape future systems, addressing deficiencies and optimizing design based on historical insights.
??? note "Changes in the ecosystem"
    The software development ecosystem is marked by `constant change, making predictions challenging`. Tools and technologies that were once unheard of can quickly become industry standards. For example, the rapid rise of `Kubernetes`, which few anticipated a few years ago, illustrates the unpredictable nature of ecosystem changes.
??? note "Introduction of New Capabilities"
     `When new capabilities arise, architecture may not merely replace one tool with another but rather shift to an entirely new paradigm`. Unexpected advancements, such as the introduction of containerization with Docker, have profound impacts on architects, tools, and engineering practices. `Architects must not only monitor new tools but also remain open to paradigmatic changes that might redefine their approach`.
??? note "Accelerated Rate of Change"
    The rate of change in the ecosystem continues to accelerate, driven by the emergence of new tools, engineering practices, and capabilities. `Architects operate in a state of constant flux, adapting to evolving trends and staying agile in response to ongoing transformations`.
??? note "Domain changes"
    `Changes in the business domain, driven by factors like business evolution or mergers, can influence the architectural choices made by developers`.
??? note "Technology changes"
    Organizations strive to keep up with technological advancements that offer obvious benefits. `Adopting technologies with clear advantages becomes a strategic move for staying competitive`.
??? note "External factors"
    External factors, such as changes in licensing costs, `may force architects and developers to reconsider their tooling choices and migrate to alternative options`.

## Decision Criteria

When architects embark on the journey of `selecting an architectural style`, they must carefully weigh various `factors that contribute to shaping the structure of the domain design`. At its core, an architect is tasked with designing two fundamental elements: `the specified domain and all the supporting structural elements essential for the system's success`.

Architects should approach the decision-making process with a clear understanding of the following key aspects:

??? note "Understanding the Domain"
    `While architects don't need to be domain experts, they must grasp critical aspects of the domain`, particularly those influencing operational architecture characteristics.

??? note "Identifying Architecture Characteristics"
    `Discovering and articulating the architecture characteristics essential to support the domain and external factors is crucial`.

??? note "Data Architecture"
    `Collaboration between architects and database administrators is vital for addressing database, schema, and other data-related concerns`. Architects must comprehend the potential impact of data design, especially when dealing with legacy data architectures.

??? note "Organizational Factors"
    External factors, such as the cost of cloud vendors or organizational plans for mergers and acquisitions, can significantly influence design decisions. `Architects need to align their designs with practical considerations`.

??? note "Knowledge of Process, Teams, and Operational Concerns"
    Project-specific factors, including the software development process, collaboration with operations, and the QA process, `play a pivotal role in influencing architectural decisions`.

??? note "Domain/Architecture Isomorphism"
    This concept explores how the structural characteristics of an architecture correspond to a particular architecture style. `Some domains naturally match certain architectural topologies, while others may be ill-suited for specific styles`.

    For instance, the `microkernel architecture style perfectly fits a system requiring customizability`, allowing architects to design plug-in customizations. Another example is genome analysis, where numerous discrete operations are essential, making space-based architecture with multiple discrete processors an ideal choice. Conversely, `some problem domains are inherently incompatible with specific architecture styles`. Highly scalable systems, for example, face challenges with large monolithic designs, as supporting numerous concurrent users becomes complex in a tightly coupled code base. 

Considering these aspects, `architects must make several key determinations`:

!!! info "Monolith vs Distributed Architecture"
    `Deciding whether a single set of architecture characteristics suffices or if different parts of the system require diverse characteristics is crucial`. A monolith may be suitable for a unified set, while distributed architecture becomes necessary for diverse characteristics.

!!! info "Data Storage Decisions"
    In a monolithic architecture, a single relational database or a few may suffice, while in a distributed architecture, `architects must decide where data should reside and how it flows throughout the system`.

!!! info "Communication Styles between Services—Synchronous or Asynchronous?"
    `Determining the communication style between services is the next consideration`. While synchronous communication is more convenient, asynchronous communication offers unique benefits but comes with its set of challenges.

`The output of this design process encompasses the architecture's topology`, including the chosen style and hybridizations, architecture decision records documenting critical design aspects, and architecture fitness functions safeguarding essential principles and operational characteristics.

# Identifying Architectural Characteristics

It's really important identifying architectural characteristics to `start creating or checking an existing architecture`. To figure out the right architectural stuff, an architect needs to `understand the domain problem well`. Also, working together with domain stakeholders is crucial to `decide what really matters`.

To find the architectural features in a project, there are at least three ways: you can get them from `domain concerns, project requirements, and and implicit domain knowledge`.

## Extracting Architecture Characteristics from Domain Concerns

An architect must be able to `translate domain concerns to identify the right architectural characteristics`. By `understanding the key domain goals and domain situation`, the architect can `turn those worries into features`. These features then guide the smart choices for the architecture.

One tip is when working with the domain stakeholders to decide the important architecture features, `try to keep the list of architectural characteristics short`. `Every feature added makes the design more complex and that's risky`. Don't get caught up in the number of features, but rather `focus on keeping the design simple`.

### Architects vs Stakeholders

When architects and stakeholders are figuring out which architecture characteristics to focus on, it's a good idea to `let domain stakeholders choose the top three most important ones`. This `helps avoid problems since not everyone agrees` on the priority of each characteristic. This way, it's easier to `find common ground and helps the architect analyze trade-offs when making vital architecture decisions`.

Most of the time, `architecture characteristics come from talking to key domain stakeholders and working together to figure out what matters`. The challenge is that architects and domain stakeholders use different terms. Architects talk about things like scalability and interoperability, while domain stakeholders talk about stuff like user happiness and getting things done quickly. The table below helps translate from domain concerns to architecture characteristics.

| Domain concern  | Architecture characteristics |
| ------------- | ------------- |
| Mergers and acquisitions | Interoperability, scalability, adaptability, extensibility |
| Time to market | Agility, testability, deployability |
| User satisfaction | Performance, availability, fault tolerance, testability, deployability, agility, security |
| Competitive advantage | Agility, testability, deployability, scalability, availability, fault tolerance |
| Time and budget | Simplicity, feasibility |

> Translate from domain concerns to architecture characteristics from [Fundamentals of Software Architecture.](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

However, it's important to note that t`his translation isn't a strict rule to blindly follow`. This is a common pitfall that many architects encounter when translating domain concerns. Being agile doesn't always mean getting to the market quickly. Time to market is a mix of agility, testability, and deployability. `Concentrating solely on one characteristic can lead to issues when trying to achieve goals`. For instance, focusing solely on performance when delivering a feature might cause availability problems when needed. And if the domain grows, will the system be able to scale?

## Extracting Architecture Characteristics from Requirements

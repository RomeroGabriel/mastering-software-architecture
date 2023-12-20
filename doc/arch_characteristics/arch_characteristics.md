# Architecture Characteristics

Architects must account for numerous factors when designing a software solution, including:

1. Auditability;
1. Performance;
1. Security;
1. Requirements;
1. Data;
1. Legality;
1. Scalability;

In software architecture, architects may collaborate on defining domain or business requirements. However, a `key responsibility involves identifying, discovering, and analyzing all the tasks that the software must perform beyond the domain functionality` – these are known as architectural characteristics. Architectural characteristics are sometimes referred to as `nonfunctional requirements`.

Architecture characteristics can be divided into `implicit` and `explicit` types. Implicit characteristics, such as `availability, reliability, and security`, often `don't explicitly appear in requirements but are crucial` for project success. Architects must leverage their `domain knowledge` to unveil these characteristics during the analysis phase. For instance, a high-frequency trading firm might not explicitly mention low latency, but architects familiar with that domain understand its critical significance.

An architectural characteristic meets three criteria:

1. It specifies a design consideration unrelated to the domain.
1. It impacts a structural aspect of the design.
1. It is crucial or significantly contributes to the success of the application.

## Criteria for Architectural Characteristics

### Specifies a Nondomain Design Consideration

Architecture characteristics `define criteria for the successful operation and design of a system`. They outline `how requirements will be implemented and justify design choices`. For example, one common and significant architectural characteristic involves defining a specific performance level for the application. Often, this level of performance `isn't explicitly stated in the initial requirements document`.

### Influences Some Structural Aspect of the Design

Architects primarily focus on `describing architectural characteristics in projects` to address design considerations: `does a specific characteristic demand distinct structural attention for its success?` Take security, for instance - while it's a concern in nearly every project, basic precautions are usually integrated during design and coding. However, it becomes an architectural characteristic when the architect must devise something unique to address it, for example integrate an external payment processor.

### Is critical or important to application success

Applications have the potential to accommodate numerous architectural characteristics, but this should be approached with caution. `Each added characteristic introduces complexity to the design`. Therefore, a vital task for architects is to focus on `selecting a minimal set of architecture characteristics rather than striving for the maximum possible`.

## Architectural Characteristics (Partially) Listed

Architecture characteristics span from low-level code attributes to sophisticated operational concerns, such as scalability and elasticity. Additionally, as the software ecosystem evolves rapidly, new concepts, tools, and terms emerge, introducing novel characteristics. Operational architecture characteristics often `closely align with operations and DevOps considerations`, representing a significant intersection of these concerns within numerous software projects.

### Operational Architecture Characteristics

Operational architecture characteristics encompass capabilities such as performance, scalability, elasticity, availability, and reliability.

| Tern  | Definition |
| ------------- | ------------- |
| Availability  | How long the system will need to be available.  |
| Continuity  | Disaster recovery capability.  |
| `Performance`  | Involves stress testing, peak analysis, frequency of function usage, response times, etc. Can demand a dedicated effort and time.  |
| Recoverability  | Ensuring business continuity during disasters: How swiftly can recovery be achieved? This influences backup strategies and hardware redundancy needs.  |
| `Reliability/safety`  | Assess if the system needs to be fail-safe, or if it is mission critical in a way that affects lives. If it fails, what's happen?  |
| Robustness  | Ability to handle error and boundary conditions while running.  |
| `Scalability`  | Ability for the system to perform and operate as the number of users or requests increases.  |

### Structural Architecture Characteristics

These characteristics focus on code structure. Architects often bear the responsibility for code quality, including modularity, controlled component coupling, readability, and various internal quality evaluations.

| Tern  | Definition |
| ------------- | ------------- |
| `Configurability`  | Ability for the end users to easily change aspects of the software’s configuration (through usable interfaces).  |
| `Extensibility`  | How important it is to plug new pieces of functionality in.  |
| `Installability`  | Ease of system installation on all necessary platforms.  |
| `Leverageability/reuse`  | Ability to leverage common components across multiple products.  |
| Localization  | Support for multiple languages.  |
| `Maintainability`  | How easy it is to apply changes and enhance the system?  |
| `Portability`  | Platforms that the system must support.  |
| Upgradeability  | Ability to easily/quickly upgrade from a previous version.  |

### Cross-Cutting Architecture Characteristics

Architecture characteristics that lack a definitive categorization yet form important design constraints and considerations.

| Tern  | Definition |
| ------------- | ------------- |
| Accessibility  | Access to all your users, including those with disabilities like colorblindness or hearing loss.  |
| Archivability  | Will the data need to be archived or deleted after a period of time? (For example, delete a user after three months inactive) |
| `Authentication`  | Security requirements to ensure users are who they say they are.  |
| `Authorization`  | Security requirements to ensure users can access only certain functions within the application.  |
| Legal  | What legislative constraints is the system operating in.  |
| Privacy  | Ability to hide transactions from internal company employees (encrypted transactions so even DBAs and network architects cannot see them).  |
| `Security`  | Does the data need to be encrypted in the database? Encrypted for network communication between internal systems? What type of authentication needs to be in place for remote user access?  |
| `Supportability`  | What level of technical support is needed by the application? What level of logging and other facilities are required to debug errors in the system?  |
| Usability/achievability  | Level of training required for users to achieve their goals.  |

### ISO Architecture Characteristics List

It's basically impossible to list all characteristics, and many of the definitions overlap. The [ISO's list](https://iso25000.com/index.php/en/iso-25000-standards/iso-25010) describes some other characteristics as well.

## Trade-Offs and Define Architecture

Applications `can only support a subset` of the architecture characteristics due to various reasons. First, each supported characteristic `requires design effort and possibly structural support`. Second, a significant challenge arises from the fact that `each architecture characteristic often impacts others`, as seen in the example of security versus performance. Hence, architects rarely find themselves in a situation where they can design a system that maximizes every single architecture characteristic.

Architects `should aim to design architecture that is as iterative as possible`. By enabling easier changes to the architecture, there's `less pressure to discover the exact correct solution` in the initial attempt. One of the crucial lessons from Agile software development is the value of iteration, which holds true across all levels of software development, including architecture.

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

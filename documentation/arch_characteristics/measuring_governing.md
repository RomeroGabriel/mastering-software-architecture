# Measuring and Governing Architecture Characteristics

## Measuring Architecture Characteristics

Organizations often encounter various `common challenges when defining architecture characteristics`:

1. ??? info "They aren’t physics"
    Numerous commonly used `architecture characteristics have unclear definitions`. For instance, what exactly does it mean for an architect to design for agility or deployability?
1. ??? info "Wildly varying definitions"
    Even within the same organization, it can be challenging to establish a shared understanding of features like performance.
1. ??? info "Too composite"
    Many important `architecture characteristics actually consist of several smaller components.` For example, when we talk about agility, it involves things like modularity, deployability, and testability that contribute to it.

`Having clear and precise definitions for architecture characteristics` addresses these issues effectively. When an organization universally agrees on concrete definitions for these characteristics, it `establishes a shared language for discussing architecture`. Furthermore, by promoting objective definitions, teams can break down complex characteristics into specific, measurable features that they can define objectively.

### Operational Measures

Numerous measurements have `nuanced interpretations depending on their specific goals`. Take, for instance, `measuring performance through the average response time for certain requests` – a prime example of operational architecture characteristics measurement. However, if teams solely focus on the average, they might `miss outliers caused by specific boundary conditions`, where 1% of requests take significantly longer than others. Hence, teams may also find it valuable to measure maximum response times to capture these outliers.

??? info "The variety of performance"
    Keep performance as example, architects and DevOps engineers have put in significant effort to `create performance budgets`, which are precise limits for various aspects of the application. For instance, an `ideal first-page render time` is set at 500 milliseconds—half a second.

    Some of these metrics also carry `further implications for application design`. Forward-looking organizations often set size-based budgets for page downloads: a maximum limit for the amount of bytes allocated to libraries and frameworks on a given page.

Top-tier teams don't just pick performance numbers out of thin air. `They use stats`. For example, say a video streaming service wants to monitor scalability. `Rather than set an arbitrary number as the goal, eengineers measure scalability over time, create statistical models, and sound alarms if real-time stats diverge from predictions.` A failure implies either a flawed model (good to know) or a problem (also good to know).

### Structural Measures

Structural measures, unlike performance, `deal with code quality`, and unfortunately, we `don't have comprehensive metrics for internal code quality yet`. Nevertheless, there are some metrics and common tools that architects can use to address important aspects of code structure.

??? info "Cyclomatic Complexity Metric"
    [Cyclomatic Complexity (CC)](https://en.wikipedia.org/wiki/Cyclomatic_complexity) is a `code-level metric`. It offers a `quantifiable way to assess code complexity`, whether it's at the function/method, class, or application level.

    It is computed by `applying graph theory to code, specifically decision points, which cause different execution paths`. For example, if a function has no decision statements (such as if statements), then CC = 1. If the function had a single conditional, then CC = 2 because two possible execution paths exist.

Architects and developers universally recognize that `excessively complex code is a code smell`. It undermines almost all the positive traits of codebases, like modularity, testability, deployability, and more. However, if teams `neglect monitoring the gradual increase in complexity, it can eventually overpower the entire codebase`.

### Process Measures

Certain `architecture characteristics align with software development processes`. Agility, for instance, is frequently seen as a valuable trait. Nevertheless, `it's a composite architecture characteristic that architects may break down into features like testability and deployability`.

??? info "Testability"
    `Testability can be quantified using code coverage tools in testing`. However, it's essential to note that, like all software checks, `it cannot substitute critical thinking and intention`. For instance, a codebase might achieve 100% code coverage but still have weak assertions that don't genuinely ensure code correctness. Nonetheless, `testability is clearly an objectively measurable characteristic`.

??? info "Deployability"
    Teams can measure deployability via a variety of metricslike the success-to-failure deployment ratio, deployment duration, and more. `Teams need to determine suitable measurements that provide valuable data for their organization, focusing on quality and quantity`. These measurements often align with team priorities and objectives.

`Agility and its related aspects are closely tied to the software development process`. However, this process `can also influence the architecture's structure`. For instance, `if easy deployment and testability are high priorities, architects may focus more on robust modularity and isolation in the architecture` – an example of an architecture characteristic influencing a structural choice.

## Governance and Fitness Functions

### Governing Architecture Characteristics

### Fitness Functions

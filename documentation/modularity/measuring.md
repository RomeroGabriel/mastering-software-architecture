# Measuring Modularity

## Cohesion

Cohesion is a `measure of the relationship between parts within a module`. In an ideal scenario, a cohesive module contains parts that `should remain together` since breaking them into smaller pieces would result in increased coupling between modules.

Cohesion measures can be ranked from best to worst:

1. **Functional Cohesion**: `Every part of the module is related to the other`, and the module contains everything essential to function.

1. **Sequential Cohesion**: Two modules interact, where `one outputs data that becomes the input for the other.`

1. **Communicational Cohesion**: Two modules form a communication chain, `where each operates on information and/or contributes to some output`. For example, add a record to the database and generate an email based on that information.

1. **Procedural Cohesion**: Two modules `must execute code in a particular order`.

1. **Temporal Cohesion**: Modules are related based on timing dependencies. For example, many systems have a list of seemingly unrelated things `that must be initialized at system startup.` These different tasks are temporally cohesive.

1. **Logical Cohesion**: The data within modules is `related logically but not functionally`. A common example of this type of cohesion exists in Java in the form of the StringUtils package: `a group of static methods that operate on String but are otherwise unrelated.`

1. **Coincidental Cohesion**: Elements in a module are not related other than `being in the same source file.` This represents the most negative form of cohesion.

Cohesion is a `less precise metric compared to coupling`, often left to the discretion of the architect. Consider this module definition:

```python title="customer_maintenance.py"
class CustomerMaintenance:
    def add_customer():
        ...

    def update_customer():
        ...

    def get_customer():
        ...

    def get_customer_orders():
        ...

    def cancel_customer_orders():
        ...
```

OR

```python title="customer_order_maintenance.py"
class CustomerMaintenance:
    def add_customer():
        ...

    def update_customer():
        ...

    def get_customer():
        ...


class OrderMaintenance:
    def get_customer_orders():
        ...

    def cancel_customer_orders():
        ...
```

There isn't a one-size-fits-all answer. It depends.

- Consider if these are the `only two operations for OrderMaintenance`; if so, collapsing them into CustomerMaintenance might be appropriate.

- Is Customer Maintenance expected to grow much larger, encouraging developers to look for opportunities to extract behavior?

- `Does OrderMaintenance require so much knowledge of Customer` information that separating the two modules would require a high degree of coupling to make it functional?

These questions represent the `trade-off analysis` at the core of a software architect's role. It involves `balancing cohesion and coupling to design an effective and maintainable system`.

## Coupling

We have effective tools to analyze coupling in code bases, which rely on `graph theory`. By considering method calls and returns as a call graph, we can perform mathematical analysis to measure coupling.

Two essential metrics are `afferent` and `efferent` coupling. `Afferent` coupling quantifies the number of `incoming connections` to a code artifact (such as a component, class, or function). `Efferent` coupling, on the other hand, measures the `outgoing connections` to other code artifacts. These metrics provide valuable insights into the relationships and dependencies among different parts of the codebase.

### Abstractness

Abstractness is a metric that `calculates the ratio of abstract artifacts` (such as abstract classes and interfaces) `to concrete artifacts` (actual implementations). It provides a measure of `how much a codebase is focused on abstract concepts versus concrete implementations`.

For instance, a codebase with no abstractions and just a large, monolithic function lacks abstractness. On the other hand, a codebase with an excessive number of abstractions can become hard for developers to comprehend and navigate, affecting its overall maintainability.

### Instability

The instability metric assesses the volatility of a codebase. A `highly unstable codebase is prone to breaking when modified`, usually due to excessive coupling. For instance, if a class relies heavily on other classes to delegate tasks, it becomes vulnerable to disruptions when any of the called methods undergo changes. High instability indicates that the codebase is more `likely to experience adverse effects from alterations, making it less resilient to changes`.

### Distance from the Main

The distance metric is a derived metric based on instability and abstractness. It envisions an ideal relationship between these two factors, aiming to find the optimal balance between them.

### Connascence

> Two components are connascent if a change in one would require the other to be modified in order to maintain the overall correctness of the system.

To now more about:

1. [Connascence: Rules for good software design](https://www.maibornwolff.de/en/know-how/connascence-rules-good-software-design/)

1. [Connascence](https://en.wikipedia.org/wiki/Connascence)

#### Static Connascence

Static connascence is a measure of `source-code-level coupling`. Architects assess the types of static connascence to determine the degree of coupling, whether afferent (incoming) or efferent (outgoing).

#### Dynamic Connascence

Dynamic connascence is a metric that `analyzes calls at runtime`, focusing on how different parts of the software interact with each other during execution. It helps architects understand the runtime coupling and dependencies between various components and modules, providing insights into `potential performance bottlenecks and areas for optimization`.

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

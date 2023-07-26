# Modularity

> 95% of the words [about software architecture] are spent extolling the benefits of “modularity” and that little, if anything, is said about how to achieve it.

Modularity is a `fundamental organizing principle` in software architecture. If an architect neglects how the components of a system interconnect, it can lead to numerous problems.

Although the concept of modularity is widely recognized in software architecture, it can be elusive to precisely define. These modules serve as a `means of encapsulating functionality, promoting code organization, and enhancing maintainability`.

Maintaining good modularity embodies an `implicit architectural characteristic`: most projects may not explicitly demand the architect to ensure it, but **sustainable code bases necessitate order and consistency in modular distinction and communication**. A well-organized system with clear boundaries between modules fosters code reusability, ease of maintenance, and scalability, contributing to the long-term success of the project.

## Definition

Modularity refers to the `logical grouping of related code`, whether it's classes in an object-oriented language or functions in a structured or functional language. Developers commonly employ modules to organize and group related code together.

For architects, understanding how developers package code is crucial, as it significantly impacts the architecture. `Tight coupling between packages can make it challenging to reuse one of them for related tasks`.

## Measuring Modularity

### Cohesion

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

### Coupling

A

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

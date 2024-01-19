# System Design

`System design is a meticulous process encompassing the definition of architecture, components, modules, interfaces, and data to fulfill specific requirements`. `This entails the translation of user needs into detailed blueprints, providing guidance for the implementation phase`. The goal is to create a well-organized and efficient structure that meets the intended purpose. Factors such as scalability, maintainability, and performance are carefully considered throughout this design journey.

## Goal

The objectives of system design include `practicality`, `accuracy`, `completeness`, `efficiency`, `reliability`, `optimization`, and `scalability`.

!!! note "Practicality"
    Practicality ensures the system targets the right audience.

!!! note "Accuracy"
    Accuracy means the system should fulfill all `functional and non-functional requirements`.

!!! note "Completeness"
    Completeness implies the system should meet all user requirements.

!!! note "Efficiency"
    Efficiency requires the system design not to overuse resources or underuse them.

!!! note "Reliability"
    Reliability ensures the system operates in a failure-free environment for a certain period.

!!! note "Optimization"
    Optimization involves optimizing time and space for individual components to work in the system efficiently.

!!! note "Scalability"
    Scalability ensures the system is adaptable with time as per different user needs.

## Steps, Techniques, and Methodologies

!!! note "Requirements"
    This step involves `gathering information` about the `problem space`, `performance requirements`, `scalability needs`, and `security concerns`. You need to `understand what the system is supposed to do`, who `will use it`, and `how it should perform`. More information in [requirements](requirements.md#requirements) section.

!!! note "Identify Major Components"
    `Determine the relationships between different components and how they contribute to the overall functionality of the system`. You break down the system into smaller parts, identify their interactions, and understand how they collectively `achieve the desired functionality`. This could involve creating diagrams or models to visualize the system's structure.

!!! note "Choose Appropriate Technology"
    Based on the requirements and components identified, you `choose the appropriate hardware and software platforms`, `databases`, `programming languages`, and `tools`. This decision `depends on various factors` like `cost`, `performance`, `scalability`, and the `expertise available`. You need to `balance the trade-offs between these factors`.

!!! note "Design Data Model"
    This involves designing the data model for the system, including the `schema for the database`, the `structure of data files`, and the `data flow between components`. The data model is central to the functioning of the system, as it `determines how data is stored`, `retrieved`, and `processed`. You need to `consider factors like data integrity`, `consistency`, and `access patterns`.

!!! note "Define Interfaces"
    This step involves `defining the interface between different components` of the system, including `APIs`, `protocols`, and `data formats`. The interface is `crucial for communication and interaction between different parts` of the system. You need to `decide how data will be passed` between components, `how errors will be handled`, and `how the system will respond to different events`.

!!! note "Capacity Estimates"
    It involves `estimating the maximum load that a system can handle`, including the number of users, transactions, or data that the system can process `without performance degradation`. Effective capacity planning `can help avoid bottlenecks`, `ensure system scalability`, and prevent costly resource over-allocation. More information in [capacity plan](capacity_plan.md#capacity-plan) section.

!!! note "Test and Validate"
    After the design is finalized, you `test the system with realistic data and use cases`. This helps to identify any issues or bottlenecks in the system. `You need to ensure that the system meets all the requirements and performs well under different conditions`. Any issues found during testing are addressed and the design is validated.

!!! note "Deploy and Maintain the System"
    After the design has been tested and validated, the system is `deployed`. However, the system needs to be `maintained over time`, including fixing bugs, updating components, and adding new features as needed. This involves `monitoring` the system's `performance`, making necessary adjustments, and planning for `future improvements`.

<!-- 
- System Design prática:
    - Chekcar Ponto único de falha
    - Lentidão no sistema
    - Garantir escalabilidade
    - Garantir performance
    - https://nealford.com/katas/list.html
    - https://www.architecturalkatas.com/index.html
-->

## References

1. [What is System Design – Learn System Design](https://www.geeksforgeeks.org/what-is-system-design-learn-system-design/)
1. [System Design Tutorial](https://www.geeksforgeeks.org/system-design-tutorial/)
1. [The complete guide to System Design in 2024](https://www.educative.io/blog/complete-guide-to-system-design)
1. [SEH 4.0 System Design Processes](https://www.nasa.gov/reference/4-0-system-design-processes/)

<!-- https://www.phind.com/search?cache=dpyqfx0bzr047uhi0dllwnwk -->
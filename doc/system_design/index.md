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
    This step involves `gathering information` about the `problem space`, `performance requirements`, `scalability needs`, and `security concerns`. You need to `understand what the system is supposed to do`, who `will use it`, and `how it should perform`. More information in [requirements](#requirements) section.

!!! note "Identify Major Components"
    `Determine the relationships between different components and how they contribute to the overall functionality of the system`. You break down the system into smaller parts, identify their interactions, and understand how they collectively `achieve the desired functionality`. This could involve creating diagrams or models to visualize the system's structure.

!!! note "Choose Appropriate Technology"
    Based on the requirements and components identified, you `choose the appropriate hardware and software platforms`, `databases`, `programming languages`, and `tools`. This decision `depends on various factors` like `cost`, `performance`, `scalability`, and the `expertise available`. You need to `balance the trade-offs between these factors`.

!!! note "Design Data Model"
    This involves designing the data model for the system, including the `schema for the database`, the `structure of data files`, and the `data flow between components`. The data model is central to the functioning of the system, as it `determines how data is stored`, `retrieved`, and `processed`. You need to `consider factors like data integrity`, `consistency`, and `access patterns`.

!!! note "Define Interfaces"
    This step involves `defining the interface between different components` of the system, including `APIs`, `protocols`, and `data formats`. The interface is `crucial for communication and interaction between different parts` of the system. You need to `decide how data will be passed` between components, `how errors will be handled`, and `how the system will respond to different events`.

!!! note "Capacity Estimates"
    It involves `estimating the maximum load that a system can handle`, including the number of users, transactions, or data that the system can process `without performance degradation`. Effective capacity planning `can help avoid bottlenecks`, `ensure system scalability`, and prevent costly resource over-allocation.

!!! note "Test and Validate"
    After the design is finalized, you `test the system with realistic data and use cases`. This helps to identify any issues or bottlenecks in the system. `You need to ensure that the system meets all the requirements and performs well under different conditions`. Any issues found during testing are addressed and the design is validated.

!!! note "Deploy and Maintain the System"
    After the design has been tested and validated, the system is `deployed`. However, the system needs to be `maintained over time`, including fixing bugs, updating components, and adding new features as needed. This involves `monitoring` the system's `performance`, making necessary adjustments, and planning for `future improvements`.

## Requirements

Requirements in system design refer to the `specifications that define what the system should do and how it should behave`. There are two main types of requirements: functional and non-functional. Both functional and non-functional requirements are `vital for a successful` system design. They guide the development process, helping to `ensure that the system meets the needs of its users and achieves its intended purpose`.

### Functional Requirements

Functional requirements `specify what a system must do`. `They are essentially the behaviors of the system and define the system's functionality`. They are usually `stated in terms of user actions or events` that the system should respond to.

!!! example
    The system should allow users to create accounts and log in using credentials like email and password or through social media integration.

### Non-Functional Requirements

Non-functional requirements `define how the system should perform`. They are not related to the system's functionality but rather `define the system's behavior`. They are crucial for ensuring the system's usability, reliability, and efficiency, often influencing the overall user experience.

!!! example
    1. Performance (e.g., the system should load within 3 seconds when the number of simultaneous users exceeds 10,000)
    1. Security (e.g., emails should be sent with a latency of no greater than 12 hours from such an activity)
    1. Usability (e.g., the system should be user-friendly and meet users' needs).

### CAP Theorem

The CAP theorem is a `concept in distributed systems that states a system can only guarantee two out of the following three properties`: Consistency, Availability, and Partition Tolerance.

!!! note "Consistency"
    `Every read receives the most recent write or an error`. In other words, `all nodes see the same data at the same time`. This means that `any data written to the system will be immediately visible` to all subsequent reads.

!!! note "Availability"
    `Every request receives a non-error response, without the guarantee that it contains the most recent write`. This means that even if the system cannot find the most current data, it still responds to requests instead of failing.

!!! note "Partition Tolerance"
    `The system continues to operate despite arbitrary partitioning due to network failures`. This means that the `system remains operational even if some of the nodes are unable to communicate with others`.

The CAP theorem states that in the event of a `network partition`, a system can `only guarantee two of these three properties`. For example, if a system is designed to prioritize availability and partition tolerance, `it may serve stale data to ensure that every request receives a response`, even if that data is not the most recent. On the other hand, if a system is designed to prioritize consistency and partition tolerance, `it may refuse to respond to requests if it cannot verify the data's consistency` across all nodes.

It's important to note that the CAP theorem `does not imply that it's impossible to build a system that satisfies all three properties`. Rather, it `states that in the face of a network partition, a system can only guarantee two out of the three properties`. Therefore, when designing a `distributed system`, developers must make a conscious decision about which two properties they want to prioritize.

## References

1. [What is System Design – Learn System Design](https://www.geeksforgeeks.org/what-is-system-design-learn-system-design/)
1. [System Design Tutorial](https://www.geeksforgeeks.org/system-design-tutorial/)
1. [The complete guide to System Design in 2024](https://www.educative.io/blog/complete-guide-to-system-design)
1. [SEH 4.0 System Design Processes](https://www.nasa.gov/reference/4-0-system-design-processes/)
1. [Functional vs Non Functional Requirements](https://www.geeksforgeeks.org/functional-vs-non-functional-requirements/)
1. [What are Non Functional Requirements — With Examples](https://www.perforce.com/blog/alm/what-are-non-functional-requirements-examples)
1. [What is the CAP theorem?](https://www.ibm.com/topics/cap-theorem)
1. [System design fundamentals: What is the CAP theorem?](https://www.educative.io/blog/what-is-cap-theorem)

<!-- https://www.phind.com/search?cache=dpyqfx0bzr047uhi0dllwnwk -->
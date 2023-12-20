# Expectations of an Architect

Defining the role of a software architect can be challenging, as it encompasses various aspects. However, it is essential to outline the **expectations and responsibilities** associated with the architect's role.

- Make architecture decisions
- Continually analyze the architecture
- Keep current with latest trends
- Ensure compliance with decisions
- Diverse exposure and experience
- Have business domain knowledge
- Possess interpersonal skills
- Understand and navigate politics

-----

## Make architecture decisions

> An architect is expected to define the [architecture decisions](https://romerogabriel.github.io/mastering-software-architecture/basic/whats_software_arc/#architecture-decisions) and [design principles](https://romerogabriel.github.io/mastering-software-architecture/basic/whats_software_arc/#design-principles) used to guide technology decisions within the team, the department, or across the enterprise.

When it comes to making architecture decisions, **guidance is crucial**. Instead of strictly specifying technology choices, the role of an **architect  should guide rather than specify technology choices**.

For instance, rather than explicitly stating that React.js should be used for the frontend, **which is a technical decision**, the architect should **guide development teams towards choosing** a reactive-based framework for the frontend, offering options like Angular, React.js, Vue.js, and others. It is important to assess whether the **architecture decision is guiding teams** to make their own technical choices or if it imposes a specific technology upon them, which may hinder their decision-making process.

While the role of an architect primarily focuses on guiding rather than specifying technology choices, there are situations where specific technology decisions become necessary to **preserve a particular architectural characteristics** like scalability, performance, or availability. Even though these decisions involve choosing a particular technology, they still fall within the realm of architectural decisions.

However, it's important to acknowledge that finding the right decision in such cases can be challenging. The topic of making architecture decisions will be further explored and discussed in subsequent sections.

-----

## Continually analyze the architecture

> An architect is expected to continually analyze the architecture and current technology environment and then recommend solutions for improvement.

This responsibility refers to **architecture vitality**, analyzing how well the **architecture can sustain itself over time**. It is not a common concern, as many architectures e**ncounter structural decay** when developers introduce code or design changes that affect the required architectural characteristics.

Additionally, **testing and release environments often tend to be overlooked** in this context. If the testing and release processes consume excessive time, it becomes challenging to achieve overall agility in the architecture.

-----

## Keep current with latest trends

> An architect is expected to keep current with the latest technology and industry trends.

Keeping up with the latest trends is crucial for staying relevant in the field of architecture. The **decisions made by an architect often have long-lasting effects and can be challenging to modify later on**. By actively staying informed about and embracing key trends, architects can **better prepare for the future and make well-informed decisions** that align with industry advancements. This proactive approach ensures that architectural decisions are forward-thinking and capable of meeting evolving needs and challenges.

-----

## Ensure compliance with decisions

> An architect is expected to ensure compliance with architecture decisions and design principles.

One of the key responsibilities of an architect is to ensure that d**evelopment teams are following the architecture decisions and design principles**. By enforcing compliance, the architect **helps prevent violations that could compromise the desired architectural characteristics** and impede the expected functionality of the application or system.

For instance, consider a scenario where there is a restriction on database access, allowing only the business and services layers (excluding the presentation layer) to communicate with the database. This architectural decision necessitates passing through all layers, even for a simple query originating from the presentation layer. However, **this decision serves a specific purpose: to control changes**. By enforcing this approach, database modifications can be implemented without affecting the presentation layer, thus ensuring a greater degree of flexibility and mitigating potential disruptions.

-----

## Diverse exposure and experience

> An architect is expected to have exposure to multiple and diverse technologies, frameworks, platforms, and environments.

As an architect, it is **not necessary to be an expert in every framework, platform, or programming language**. However, it is crucial to **have a diverse exposure and familiarity with a variety of technologies**. This includes knowing how to interface with multiple systems and services based on different technologies.

A skilled software architect actively **seeks opportunities to gain experience** in various languages, platforms, and technologies. Rather than focusing solely on technical depth, it is important to **prioritize technical breadth**. For example, instead of being an expert in just one caching product, **it is more valuable for an architect to be familiar with the features, advantages, and disadvantages of multiple caching products**. This broader understanding allows for informed decision-making when choosing the most suitable caching solution for a given scenario.

By continuously **expanding their technical breadth**, an architect can effectively navigate diverse technology landscapes, make informed decisions, and **provide valuable guidance in selecting the right tools and technologies for a project**. This breadth of exposure and experience enhances their ability to design robust and scalable solutions that align with business requirements.

-----

## Have business domain knowledge

> An architect is expected to have a certain level of business domain expertise.

Having a **strong understanding of the business domain** is a fundamental expectation for an architect. Without this knowledge, it becomes challenging to **comprehend the business problem, goals, and requirements**, making it difficult to devise an effective architecture. Additionally, lacking business domain knowledge **diminishes the architect's credibility** when communicating with stakeholders and business users.

-----

## Possess interpersonal skills

> An architect is expected to possess exceptional interpersonal skills, including teamwork, facilitation, and leadership.

Being an effective software architect involves **more than just providing technical guidance**. It requires possessing **strong interpersonal skills and the ability to lead development teams through the implementation** of the architecture. In fact, leadership skills are considered equally important, if not more so, than technical expertise for a successful architect.

## Understand and navigate politics

> An architect is expected to understand the political climate of the enterprise and be able to navigate the politics.

In the realm of software architecture, it is essential for architects to possess the ability to understand and navigate the intricacies of organizational politics. While developers often have the freedom to make alterations like refactoring code using the strategy pattern **without seeking approval, architects face different challenges**.

Consider a scenario where an architect is responsible for a large customer relationship management (CRM) system and encounters issues with controlling database access from other systems. To address this, the architect decides to implement application silos, ensuring that each application's database is accessible only to the corresponding application. This decision empowers the architect to have better control over customer data, security, and change control.

However, unlike the previous developer scenario, **architectural decisions of this magnitude are likely to be met with resistance from various stakeholders** within the company. For instance, if other applications can no longer access the database directly, they would need to request data from the CRM system through remote access calls using protocols like REST or SOAP. This shift in approach **triggers challenges from different quarters**. Product owners, project managers, and business stakeholders may express concerns about increased costs or additional effort required. Developers may also challenge the decision, presenting alternative approaches they believe to be superior.

In such situations, architects must skillfully navigate the company's politics and employ **effective negotiation techniques to gain approval for their decisions**.

## References

- [Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)

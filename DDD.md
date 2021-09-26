# Domain Driven Design

Domain-Driven Design is a framework based on **strategic** value, and it’s about mapping business domain concepts into software artifacts.

Domain-driven design (DDD) is an approach to developing software for complex needs by deeply connecting the implementation to an evolving model of the core business concepts.
Its premise is:
- Place the project’s primary focus on the core domain and domain logic
- Base complex designs on a model
- Initiate a creative collaboration between technical and domain experts to iteratively cut ever closer to the conceptual heart of the problem.

![image](https://user-images.githubusercontent.com/6672785/134819021-8508c764-2b1a-4617-ae92-d0f28e6dc799.png)

## DDD Modelling process:
![image](https://user-images.githubusercontent.com/6672785/134819763-4ecdcfa4-9699-4a62-8242-6c9c6f195344.png)

### Analyze domain
A domain refers to real-world aspects of a solution (e.g., automobile, banking, mortgage, credit, debit accounts, credit cards, retails loans, content management, etc.) The domain informs the requirements and acceptance criteria for the system to be implemented by the developer.

The Domain model captures concepts and processes for a specific business domain and require a deep understanding of the field in question. 

A domain is an area that project covers; it has its terminology, ubiquitous language, requirements, and problems to solve; it is a concrete domain with its small world. The field can be automobile, banking, mortgage, credit, debit accounts, credit cards, retails loans, content management, our new project.

A domain can be decomposed into subdomains, which is one particular part of the domain. Typically reflect some organizational structure in which some users use a specific ubiquitous language. For example, automobile can be decomposed into logistics, researches & development, traders, production and marketing; where research & development itself can further be decomposed to design, CAD (computer-aided design), test, assistance systems, infotainment, product planning, and engine development, which is a good example of domain decomposition also know as subdomain.

### Define bounded contexts

A bounded context is a clear boundary around a domain model and determines the parts of the domain the model will apply on. The bonded context primarily encapsulates the ubiquitous language and its domain model, but it includes what exists to provide interaction with and support the domain model. A bounded context is a software artifact and often seen as an excellent way to scope a microservice functionality.

-   One team per Bounded Context
-   Separate code repository for each Bounded Context
-   Domain Model + DB Schema + UI + Web Services (API)
-   Subdivide large domains into smaller contexts.
-   Each context can have its own ubiquitous language and its own model.
-   Bounded Contexts may share some domain aspects.

![image](https://user-images.githubusercontent.com/6672785/134819093-48f162af-14f2-45c7-8e81-6d32440ec7bb.png)

Example:
![image](https://user-images.githubusercontent.com/6672785/134819434-49c4aac2-3c36-4b21-88f1-c70c80969dfc.png)


##### Ubiquitous Language

Ubiquitous Language  is the term uses in Domain-Driven Design for the practice of building up a common, rigorous language between developers and users. This language should be based on the Domain Model used in the software — hence the need for it to be rigorous since software doesn’t cope well with ambiguity.

![image](https://user-images.githubusercontent.com/6672785/134818847-a0f01fc5-9fd4-400d-bac0-83e6083a0d19.png)

To create an UL, have an open discussion, analyze existing documents, express the domain clearly, and define an agreed glossary. Glossary alone won't help. Use it consciously to arrive at a common understanding of the model.


##### Context Map

An enterprise application has multiple models, and each model has its own Bounded Context. It is advisable to use the context as the basis for team organization. People in the same team can communicate more easily, and they can do a better job integrating the model and the implementation. While every team works on its model, it is good for everyone to have an idea of the overall picture.

### Defines entities, aggregates, and services

The entity, value object, aggregate, services, factory, and repository are the building blocks also known as the **tactical** approach to Domain-Driven Design toward its full realization

##### Entity

We design a domain object as an Entity when we care about its individuality where we have to determine its identity correctly and how we are going to obtains it.

-   A noun with own intrinsic identity
-   Mutable — State can change over time
-   Can be associated with other entities and value objects
-   Can’t be shared
-   Entities have a history and can be traced

##### Value Object

We design domain concepts as a Value Object when we care only about the attributes of an element of the model and not in its identity; we should strive to model using Value Object instead of Entity wherever possible. To decide whether a concept is a Value, you should determine whether it possesses most of these characteristics:

-   It measures, quantifies, or describes a thing in the domain
-   It can be maintained as immutable — State can’t change
-   It models a conceptual whole by composing related attributes as an integral unit
-   It is entirely replaceable when the measurement or description changes
-   It can be compared with others using Value equality
-   It supplies its collaborators with Side-Effects-Free Behavior
-   A noun without an identity
-   Immutable — State can’t change
-   Can be associated with other entities
-   Can be shared
-   Does not have a lifespan, no history associated with them
-   Shouldn’t have their tables in the database.

![image](https://user-images.githubusercontent.com/6672785/134818951-677164cf-3eb6-42f2-b74c-d8f477b61581.png)


##### Aggregate

An aggregate is an associated cluster object which is considered as one unit (also knows as a transaction) root entity. Aggregates have a clearly defined boundary (only cares about integrity and responsibility of the object inside the aggregate, it does not care about external objects). Aggregates protect internal objects from the outside world (outside objects can only access by the root aggregate and can’t change the state of the objects in the aggregate). The aggregate has the responsibility to protect the integrity of the entities and value objects they have.

-   One root entity per aggregate
-   Associated entities can refer to root but not other entities in the aggregate
-   All operations are done through root

![image](https://user-images.githubusercontent.com/6672785/134818967-79123baa-135a-4f16-87da-e69a4f75fdac.png)


##### Service

A domain service is a stateless operation that fulfills a domain-specific task, which performs significant business process and capable of transforming a domain object from one composition to another, normal uses:

-   Services are the actions in your application
-   Services cause state changes to Entities
-   Has operations that conceptually doesn’t below to an domain object
-   Stateless
-   Interface is defined in terms of other elements of the domain model
-   A service can be part of any layer (Application, Domain, Infrastructure)
-   Still driven by name principles of Ubiquitous Language and Domain Expertise

##### Factory

The factory pattern has the responsibility for getting the needed information and constructing the object for the domain as aggregate; best usage of the factory pattern:

-   Creates the entities and value objects
-   Use only when the entity creation is complex

##### Repository

A repository encapsulates a collection of objects stored in the database.

-   Collection of entities
-   Takes care of updating an entity
-   Takes care of retrieving an already persisted entity
-   One repository per aggregate root
-   Layer abstraction that can be file, storage or in memory database

![image](https://user-images.githubusercontent.com/6672785/134818888-8612f86d-7176-4759-bc3d-511f4458d92c.png)

## DDD Layers

![image](https://user-images.githubusercontent.com/6672785/134820177-176e66b2-3f02-4c73-8986-205f6afe2e9b.png)


![image](https://user-images.githubusercontent.com/6672785/134819881-146a5e12-a683-44a0-abb1-f19aad82379a.png)


![image](https://user-images.githubusercontent.com/6672785/134820189-a15dcdba-a713-49e3-9554-4699bc230a9d.png)


## Summary:
![image](https://user-images.githubusercontent.com/6672785/134819243-6140acbc-b0ec-4663-9658-762358402f3f.png)


Reference: https://devopedia.org/domain-driven-design

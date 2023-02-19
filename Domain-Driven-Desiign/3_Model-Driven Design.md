Model-Driven Design
-

It is important to choose a model which can be easily and accurately put into code. how to we approach the transition from model to code.

One of the recommended design techniques is the so called *analysis* model.
The analysis model is the result of business domain analysis, resulting in a model which has no consideration for software used for implementation.
Such a model is used to understand the domain.
Software is not taken into account at this stage because it is considered to be a confusing factor.
Analysis models are soon abandoned after coding starts.
One of the main issues with this approach is that analysis cannot foresee some of the defects in their model, and all the intricacies of the domain.

A better approach is to closely relate domain modeling an design.
Developers should be included in the modeling process. 
Getting the developers involved provides feedback.It make sure that the model can be implemented in software.
If analyst is separated from the implementation process, he will soon lose his concern about the limitations introduced by development. 
The result is a model which is not practical.

Object-oriented programming is suitable for model implementation because they are both based on the same paradigm.

The Building Blocks Of A Model-Driven Design
-

The purpose of this patterns is to present some of the key elements of object modeling and software design from viewpoint of domain-driven design.

User-Interface -> Application -> Domain -> Infrastructure

When we create a software application, a large part of the application is not directly related to domain, but it is part of the infrastructure or serves the software itself.
It is possible and ok for domain part of an application to be quite small compared to the rest.

When domain-related code is mixed with the other layers, it becomes extremely difficult to see and think about.
Therefore, partition a complex program into layers, develop a design within each layer that is cohesive and depends only on the layer below.

User Interface(Presentation Layer): Responsible for presenting information to the user and interpreting user commands.

Application Layer: This is thin layer which coordinates the application activity. It does not contain business logic, does not hold the state of business objects, but it can hold the state of an application.

Domain Layer: This layer contains information about the domain. This is heart of the business software. The state of business objects is held here. Persistence of the business objects and possibly their states is delegated to the infrastructure layer.

Infrastructure Layer: This Layer acts as a  supporting library for all the other layers. It provides communitcation between layers, implements persistence for business objects, contains supporting libraries for the user inerface layer, etc

Entities
-

There is a category of objects which seem to have an identity, which remains the same throughout the states of the software.
For these objects it is not the attributes which matter, but a thread of continuity and identity, which spans the life of a system and can extend beyond it. Such objects are called Entity.

Implementing entities in software means creating identity.
Usually the identity is either an attribute of the object, a combination of attributes, an attribute specially created to preserve and express identity, or behavior.

When an object is distinguished by its identity, rather than its attributes, make this primary to its definition simple and focused on life cycle continuity and identity.
Define a means of distinguishing each object regardless of its form or history.
Be alert to requirements that call for matching objects by attributes.
Define an operation that is guaranteed to produce a unique result for each object
The model must define what it means to be the same thing.

Entities are important object of a domain model, and they should be considered from the beginning of modeling process.
It is also important to determine if an object needs to be an entity or not, which is discussed in the next pattern.

Value Objects
-
Entities are necessary objects in a domain model. 
Entities can be tracked. But tracking and creating identity comes with cost.
There are also performance implications in making all objects entities.

An object that is used to describe certain aspects of a domain, and which does not have identity, is named Value object.

It is recommended to select as entities only those objects which confirm to the entity definition. make the rest of the object Value Objects.

Having no identity, Value Objects can be easily created and discarded.

It is highly recommended that value objects be immutable. They are created with a constructor, and never modified during their life time.
Being immutable, and having no identity, Value object can be shared.

Immutable objects are sharable with important performance implications. They also manifest integrity.

If Value Objects are sharable, they should be immutable. Value Object should be kept thin and simple. 
when a Value Object is needed by other party, it can be simply passed by value, or copy of it can be created and given.
Value Objects are used to simply contain attributes of a domain objects, that does not mean that it should contain a long list with all the attribute.

Services
-
We discover that some aspects of the domain are not easily mapped to objects. Objects are generally considered as having attributes, an internal state which is managed by the object, and exhibit a behavior.

nouns of the language are easily mapped to objects. the verbs of the language, associated with their corresponding nouns become the part of the behavior of the objects.
But there are some actions in the domain, some verbs which do not seems to belong to any objects.
They represent an important behavior of the domain, so they cannot be neglected or simply incorporated into some of the Entities or Value Object.

When such a behavior is recognized in the domain. the best practices is to declare it as Sevice. Such an object does not have an internal state, and its purpose is to simply provide functionality for the domain.

Services act as interfaces which provide operation. Services are common in technical frameworks, but they can be used in the domain layer too.
A service is not about the object performing the service, but is related to the objects the operations are performed on/for.
In this manner, a Service usually becomes a point of connection for many objects.


A Service should not replace the operation which is normally belongs on domain logic. We should not create a Service for operation needed.
But when such an operation stands out as an important concept in the domain, a Service should be created for it.

1. The operation performed by the Service refers to a domain concept which does not naturally belong to an Entity ot Value Object
2. The operation performed refers to other objects in the domain
3. The operation is stateless

Modules
-
It is necessary to organize the model into modules. Modules are used as a method of organizing related concepts and tasks in order to reduce complexity.
software code should have a high level of cohesion and low level of coupling.
Communication cohesion is achieved when parts of the module operate on the same data. It makes sense to group them.
The functional cohesion is achieved when all parts of the module work together to perform a well-defined task.

Using modules in design is a way to increase cohesion and decrease coupling. Modules should have well defined interfaces which are accessed by other modules.

After the role of the module is decided, is usually stays unchanged, while the internals of the module may change a lot.
It is true that module refactoring may be more expensive than a class refactoring.

Aggregate
-
Aggregate is a domain pattern used to define object ownership and boundaries.

A model can contain a large number of domain objects. No matter how much consideration we put in the design. it happens that many objects are associated with on another, creating a complex net of relationship.

The challenges of models are most often not to make them complete enough. but rether to make them as simple and understandable as possible.
Most of the time it pays of to eliminate or simplify relations from the model. That is unless they embed deep understanding of domain.

1. associations which are not essential for model should be removed
2. multiplicity can be reduced by adding a constraint.
3. many times bidirectional associations can be transformed in unidirectional ones.

the system has to make sure that it is properly updated throughout the system, and data integrity is guaranteed.
Transactions are used  to enforce data integrity.

But if the model was not carefully designed, there will be a high degree of database contention.

It is also necessary to be able to enforce the invariants. The invariants are those rules which have to maintained whenever data changes. This is difficult to realize when many objects hold references to changing data objects.

It is difficult to guarantee the consistency of changes to objects in a model with complex association. Many times invariants apply to closely related objects, not just discrete ones. Yet cautious locking schemes cause multiple users to interfere pointlessly with each other and make system unusable.
Therefore, use Aggregates.

An Aggregate is a group of associated objects which are considered as one unit with regard to data change. 
The Aggregate is demarcated by a boundary which separates the objects inside from those outside.
Each Aggregate has one root. The root is an Entity. and it is the one only object accessible from outside.
The root can hold reference to any of the aggregated objects, and the other objects can hold reference only to the root object.

Since other object can hold reference only to the root, it means that they cannot directly change the other objects in the aggregate. All they can do is to change root, or ask the root to perform some actions.

If the root is deleted and removed from memory, all the other objects from the aggregate will be deleted too. Because not other object holding reference to any of them.

If objects of an Aggregate are stored in a database, only one the root should be obtainable through queries.
The root Entity has global identity, and is responsible for maintaining the invariants. Internal Entities have local identity.

This arrangement makes it practical to enforce all invariants for objects in the Aggregate and for the Aggregate as a whole in any state change.  

Factories
-
Factories are used to encapsulate the knowledge necessary for object creation, and they are especially useful to Aggregates. When a root of Aggregate is created along with it, and all the invariants are enforced.

It is important for creation process to be atomic. If it is not, there is a chance for the creation process to be half done for some objects, leaving the in an undefined state.

Therefore, shift the responsibility for creating instances of complex objects an Aggregates to a separate object, which may itself have no responsibility in the domain model but is still part of the domain design.
Provide interface and encapsulates all complex assembly and that does not require the client to reference the concrete classes of the being instantiated.

We have to make sure the Factory is updated to support the new condition(change in the model).

Repositories
-
In a model-driven design, object have a life cycle starting with creation and ending with deletion or archiving.
The purpose of which is to encapsulate all the logic needed to obtain object reference.
The overall effect is that the domain model is decoupled from the need of storing objects or their references, and accessing the underlying persistence infrastructure.

A Repository may contain detailed information used to access the infrastructure, but its interface should be simple.

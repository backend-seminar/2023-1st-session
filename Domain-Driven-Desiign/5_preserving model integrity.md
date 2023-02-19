When multiple teams work on a project, code development is done in parallel.
The first requirement of a model is to be consistent, with invariable terms and no contradiction,
internal consistency of a model is called unification.

When the design of the model evolves partially independently, we are facing the possibility to lose model integrity.
Instead of trying to keep one big model that will fall apart, we should consciously divide it into several models.

Bounded Context
-
The main idea is to define the scope of a model, to draw up the boundaries of its context, then do the most possible to keep the model unified.

A Bounded Context is not a Module. A Bounded Context provides the logical frame inside which the module evolves.

A model is not fully defined from the beginning.
That's why Continuous Integration is a necessary process within a Bounded Context.

Context Map
-
It is advisable to use the context as the basis for team organization.
A Context Map is a document which outlines the different Bounded Contexts and the relationships between them.

If the contexts are not clearly defined, it is possible they will overlap each other.
If the relationships between contexts are not outlined, there is a chance they won't work when the system is integrated.

A common practice is to define the contexts, then create modules for each context, and use a naming convention to indicate the context each module belongs to.

Shared Kernel
-
Designate some subset of the domain model that the two teams agree to share.
The explicitly shared stuff has special status, and should not be changed without consultation with other team.

The purpose of the Shared Kernel is to reduce duplication, but still keep two separate contexts. 
Development on Shared Kernel needs a lot of care.

Any change in the kernel should be communicated to another team, and the teams should be informed, making them aware of the new functionality.

Customer-Supplier
-
It is a special relationship: one depends a lot on the other.
The contexts in which those two subsystems exist are different, and the processing result of one system is fed into the other.
They do not have a Shared Kernel.
The two subsystems are in a Customer-Supplier relationship.

The two teams should meet regularly or upon request, chat as a customer does with his supplier. The customer team should present its requirements. while the supplier team should make the plans accordingly.
The interface between the two subsystem needs to be precisely defined.

Conformist
-
When two teams have a Customer-Supplier relationship in which the supplier team has no motivation to provide for the customer team's needs, the customer team is helpless.
If the customer has to use the supplier team's model, and if that is well done, it may be time for conformity.

The customer team can not make changes to the Kernel. They can only use it.

If the component has a small interface, it might be better to simply create an adapter for it, and translate between our model and the component's model.

Anticorruption Layer
-
We often encounter circumstances that we should work with legacy code or a separate application.
We can not ignore the interaction with the external model, but should isolate our own model from it.
We should build Anticorruption Layer which stands between our client model and the external one.

Anticorruption Layer talks to the external model using the external language not the client one. This layer works as a two way translator between two domain and languages.
So the client model remains pure and consistent without being contaminated by the external one.

Separate Ways
-
If we reach the conclusion that integration is more trouble than it is worth, then we should go the Separate Ways.
The Separate Ways is a pattern when app can be made ip of several smaller app which have little or nothing in common from a modeling perspective.

Before going on Separate Ways we need to make sure that we won't be coming back to an integrated system.

Open Host Service
-
If the external subsystem turns out to be used not by one client subsystem, but by several ones.
Define a protocol that gives access to your subsystem as a set of Service. 
Then use a one-off translator to augment the protocol for special needs.

Distillation
-
Distillation is the process of separating the substances composing a mixture.
The idea is to define a Core Domain which represent the essence of the domain.
The byproducts of the distillation process will be Generic Subdomain which will comprise the other parts of the domain.
Make the Core small.

Ways to implement Subdomain
-
1. Off-the-shelf Solution: having the entire solution already done by someone else.
2. Outsourcing
3. Existing Model
4. In-House implementation - Good, but costed


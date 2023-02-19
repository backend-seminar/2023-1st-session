Continuous Refactoring
-

- Design without a model can lead to software which is not true to the domain it serve, and may not have the expected behavior.
- Modeling without feedback from the design and without developers being involved leads to a model which is not well understood by those who have to implement it, and may not be appropriate for the technologies used
- Refactoring is the process of redesigning the code to make it better without changing application behavior
- Technical refactoring, the one based on patterns, can be organized and structured. 
- On the other hand, Refactoring toward deeper insight cannot be done in the same way. A good model is the result of deep thinking, insight, experience, and flair


- Few tips fot insight
  - Read the business specifications and look for nouns and verbs. nouns are converted to classes and verbs become method


- Traditionally, refactoring is described in terms of code transformations with technical motivations. Refactoring can also be motivated by an insight into the domain and a corresponding refinement of the model or its expression in code

Bring Key Concepts Into Light
-
- A Breakthrough often involves a change in thinking, in a way we see the model.  A Breakthrough may imply a large amount of refacotoring
- To reach a Breakthrough, we need to make the implicit concepts explicit. Some of the concepts may remain unnoticed at the beginning. They are implicit concepts
- We discover that some of them play a key role in the design
- First thing to discover implicit concepts is to listen to the language. If a key concept is missing from the puzzle, the others will have to replace its functionality. This will fatten up some objects, adding them behavior which is not supposed to be there. The clarity of the design will suffer
- When building knowledge it is possible to run into contradiction. Some of the contradictions may not really contradictions, but different ways of seeing the same thing.
- We should try to reconcile contradictions. Sometimes this brings to light important concepts.
- An other obvious way of digging out model is to use domain literature.
- Using Constraint also helps to make explicite and express an invariant
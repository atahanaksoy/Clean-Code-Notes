# Chapter 12: Emergence

## Getting Clean via Emergent Design

A design is simple if it follows these rules:

- **Runs all tests**
  - Systems that aren't testable aren't verifiable. A system that cannot be verified should never be deployed.
  - Making our systems testable pushes us toward a design where our classes are small and single purpose.
  - Tight coupling makes it difficult to write tests. With more tests, we improve our design by introducing abstractions.
- **Contains no duplication**
- **Expresses the intent of the programmer**
  - As systems become more complex, they take more and more time for a developer to understand, and there is an even greater opportunity for a misunderstanding. Therefore, the code should have good names, small functions and classes, well written unit-tests etc.
- **Minimizes the number of classes and methods**
  - In an effort to make our classes and methods small, we might create too many tiny classes and methods. So this rule suggests that we also *keep our function and class count low.*


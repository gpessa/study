## Solid

Five guidelines were developed by Robert C. Martin as guidelines/principles made it easy for developers to create readable and maintainable programs.

- **S**: Single Responsibility Principle
- **O**: Open-Closed Principle
- **L**: Liskov Substitution Principle
- **I**: Interface Segregation Principle
- **D**: Dependency Inversion Principle

#### Single Responsibility Principle

A class should be responsible for only one thing. If a class has more than one responsibility, it becomes coupled.
The name of a class should be specific and tell you exactly what are its responsibilities.

#### Open-Closed Principle

Software entities (Classes, modules, functions) should be open for extension, not modification.

#### Liskov Substitution Principle

It's a principle that should help to understand if you should use inheritance or not.
Means that if you create a class extending another, the one who extend should implement all the methods or the properties.

A sub-class must be substitutable for its super-class
Substitutability is a principle in object-oriented programming stating that, in a computer program, if S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e. an object of type T may be substituted with any object of a subtype S) without altering any of the desirable properties of the program (correctness, task performed, etc.)

#### Interface Segregation Principle

Make fine grained interfaces that are client specific
Clients should not be forced to depend upon interfaces that they do not use.

#### Dependency Inversion Principle

Dependency should be on abstractions not concretions
A. High-level modules should not depend upon low-level modules. Both should depend upon abstractions.
B. Abstractions should not depend on details. Details should depend upon abstractions.

# SOLID Principles

SOLID is an acronym that stands for the following:

- Single responsibility principle
- Open/closed principle
- Liskov substitution principle
- Interface segregation principle
- Dependency inversion principle

## Single Responsibility Principle
This states that a class should have a single responsibility, but more than that, a class should only have one reason to change.

[Example](/example/S/)

## Open/Closed Principle
In the open/closed principle classes should be open for extension, but closed for modification. Essentially meaning that classes should be extended to change functionality, rather than being altered.

[Example](/example/O/)

## Liskov Substitution Principle
Created by Barbara Liskov in a 1987, this states that objects should be replaceable by their subtypes without altering how the program works. In other words, derived classes must be substitutable for their base classes without causing errors.

[Example](/example/L/)
  
## Interface Segregation Principle
This states that many client-specific interfaces are better than one general-purpose interface. In other words, classes should not be forced to implement interfaces they do not use.

[Example](/example/I/)

## Dependency Inversion Principle
This states that classes should depend upon abstractions, not concretions. Essentially, don't depend on concrete classes, depend upon interfaces.

[Example](/example/D/)

## Ref
- https://www.hashbangcode.com/article/solid-principles-php

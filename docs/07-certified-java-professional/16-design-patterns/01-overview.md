# Design Pattern In Java

Design patterns are typical solutions to common problems in software design. \
They are catagogrised into 3 categories:
1. Creational
2. Structural and
3. Behavioral

## Creational Patterns

1. Singleton:
    - Ensures a class has only one instance and is shared across globally.
    - Useful for logging, configuration settings and connection pooling.

2. Factory Method:
    - Defines an interface for creating an object but lets the subclasses alter the type objects to be created.
    - Useful for creating families of related objects without specifying concrete classes.

3. Abstract Factory:
    - Defines an interface for creating families of related objects without specifying concrete classes
    - Useful for creating complex objects that depends on other objects.

4. Builder:
    - Separates the construction of a complex object from its representation, allowing the same construction process to create various representations.
    - Useful for creating complex objects step by step.

5. Prototype:
    - Creates a new object by copying an existing object known as the prototype.
    - Useful for creating objects that are expensive to create or initialize.

## Structural Patterns

1. Adapter:
    - Allows incompatible interfaces to work together.
    - Useful for integrating legacy code or third party libraries.

2. Bridge:
    - Decouples an abstraction from its implementation so that the two can vary independently.
    - Useful for separating an object's interface from its implementation.

3. Composite:
    - Composes objects into tree structures to represent part-whole hierarchies.
    - Useful to treating individual objects and composition of objects uniformly.

4. Decorator:
    - adds resposibilities to objects dynamically.
    - useful for extending the functionality of an object without altering its structure.

5. Facade:
    - Provides a simplified interface to a complex subsystem
    - Useful for simplifying complex systems and making them easier to use.

6. Flyweight:
    - Shares common data between multiple similar objects to support large number of fine-grained objects efficiently
    - Useful for reducing the memory usage when many similar objects are needed.

7. Proxy:
    - Provides a surrogate or placeholder for another object to control access to it.
    - Useful for lazy initialization, access control, and virtual proxies.

## Bahavioral Patterns

1. Chain of Resposibility
    - Passes a request along a chain of handlers
    - Useful for decoupling the sender of a request from its receiver.

2. Command
    - Encapsulates a request as an object, thereby  allowing for parameterization of clients with queues, requests and operations.
    - Useful for implementing undoable operations and transactional systems.

3. Interpreter:
    - Defines a grammer for a language and an interpreter to deal with the grammar.
    - Useful for creating simple language or domain specific languages.

 4. Iterator
    - Provides a way to access the elments of an aggregate object sequentially without exposing its underlying representation.
    - Useful for traversing collections

5. Mediator

# SOLID Principles

SOLID principles are a set of 5 design principles in object-oriented programming intended to make software design more understandable, flexible and maintanable.

SOLID is an accronym for the following design principle:

1. Single Resposibility Principle (SRP)
    - A class should have one and only one reason to change.
    - A class should have one job or responsibility.
    - Why it is recommended?
    - If it has multiple reponsibilities, it becomes bloated and changing one part might accidentally break another.

2. Open Close Priciple (OCP)
    - Software entities should be open for extension but closed for modification.
    - It is usually achieved using interfaces and abstract classes.

3. Liskov Substitution Principle (LSP)
    - Objects of a superclass should be replaceable with the objects of subclass without affecting the correctness of the program.
    - It's about ensuring that inheritance is used correctly.

4. Interface Segregation Principle (ISP)
    - No client should be forced to depend on methods it does not use.
    - Many client-specific interfaces are better than one general-purpose interface.
    - Instead IMachine think of Printable, Faxable, Scanable interfaces

5. Dependency Inversion Principle (DSP)
    - Depend upon abstractions not concretes.
    - High level modules (Business Logic) should not depend on low-level modules(database api).
    - Both should depend on abstractions and interfaces.

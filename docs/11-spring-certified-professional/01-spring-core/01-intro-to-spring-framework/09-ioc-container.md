# IOC Container

Q. How does Spring achieve Inversion of Control?

A. By IOC container.

## IOC Container - Definition

The Inversion of Control (IoC) container is the core runtime component that creates, configures and manages the lifecycle of beans. The container is responsible for instantiation, dependency injection, lifecycle callbacks and wiring.

Two commonly referenced container abstractions are:

- BeanFactory — the original, simple factory-style container (lazy, minimal features). Mostly used as a low-level reference.
- ApplicationContext — a richer container that builds on BeanFactory and adds features such as internationalization, application events, convenient resource loading, support for AOP, and integration with Spring's enterprise services. Common implementations include `AnnotationConfigApplicationContext`, `ClassPathXmlApplicationContext`, and the web-aware `AnnotationConfigWebApplicationContext`.

Exam note: when asked which container to use in typical applications, prefer `ApplicationContext` — it's what most real-world apps and Spring Boot use.

How does the container know which beans to manage?

That's where Spring Configurations come in. Let's dive it in the next section.

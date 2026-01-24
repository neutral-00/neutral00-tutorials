# Questions around Tomcat Vs Jetty

---

## Q. It is said that spring boot provides embedded servers tomcat, jetty. are they two different products or the same?

Tomcat and Jetty are two different web server/servlet container products; Spring Boot can embed either one of them, but they are not the same thing.

### What embedded server Spring Boot Provides?

Ans: Tomcat by default. but can be configured to embed Jetty instead.

Spring Boot’s “embedded server” feature just means it can package a servlet container inside your application so you run a jar and the server starts with it. By default, the `spring-boot-starter-web` starter pulls in embedded Tomcat, but you can exclude Tomcat and add Jetty or Undertow instead.

### Tomcat vs Jetty

- Tomcat is a widely used, traditional servlet container and is the default choice for most Spring Boot apps.
- Jetty is a separate implementation of the servlet and related specs, often chosen for high‑concurrency or embedded use cases, but it plays the same “type” of role as Tomcat (HTTP server + servlet container).

---

## Q. How to switch Spring Boot from embedded Tomcat to Jetty?

Switching from embedded Tomcat to Jetty in Spring Boot is done purely via dependencies: exclude Tomcat and add the Jetty starter.

### Maven configuration

In `pom.xml`, modify the web starter to exclude Tomcat and then add Jetty:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
  <exclusions>
    <exclusion>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
    </exclusion>
  </exclusions>
</dependency>

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```

If you use other starters that bring in Tomcat (e.g., Thymeleaf starter), also exclude `spring-boot-starter-tomcat` from those dependencies.

### Gradle configuration

In `build.gradle`, exclude Tomcat from the web starter and add Jetty:

```groovy
dependencies {
    implementation('org.springframework.boot:spring-boot-starter-web') {
        exclude group: 'org.springframework.boot', module: 'spring-boot-starter-tomcat'
    }
    implementation 'org.springframework.boot:spring-boot-starter-jetty'
}
```

After changing dependencies, just rebuild and run the app; Spring Boot will auto-configure Jetty as the embedded server instead of Tomcat.

---

## Q. When should jetty be preferred over tomcat?

Jetty should be preferred over Tomcat in scenarios where:

- Better handling of high concurrency and simultaneous users is critical, as Jetty's architecture with non-blocking I/O suits scalable, high-load environments well.
- Fast startup times and a smaller memory footprint are important, such as in microservices or cloud-native applications aiming for efficient resource usage and quick scaling.
- Lightweight and modular server design is desired, allowing for embedding Jetty inside applications with just the needed components without the extra overhead Tomcat may bring.
- Modern protocols like HTTP/2, WebSocket, SPDY, and asynchronous HTTP clients are priorities, where Jetty offers strong support and innovation.
- Flexible programmatic configuration (via Java or concise XML) is preferred for easier customization compared to Tomcat’s configuration approach.

Tomcat remains a strong default choice for general-purpose Java web applications and enterprise deployments due to its long track record, stability, security focus, and extensive support.

In summary, Jetty excels in microservices, cloud, lightweight embedded systems, and high-concurrency scenarios, while Tomcat suits more traditional, large-scale enterprise applications requiring proven stability and comprehensive Java EE support. The choice depends on the specific performance, deployment, and configuration needs of your project.

---

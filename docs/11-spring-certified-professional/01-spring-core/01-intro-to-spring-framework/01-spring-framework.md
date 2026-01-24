# 1.1 Introduction to Spring Framework

Spring is a comprehensive framework for building highly scalable enterprise applications.

## brief history

- introduced by Rod Johnson in 2003
- Spring framework 1.0 was release in 2004 March
- 2009 Aug - VMware purchased Spring Source for $420 Million
- 2022 Fall - Spring Framework 6 && Spring Boot 3.0 Released
  - requires JDK 17+

## Spring Vs Spring Boot

- Spring framework is a framework of libraries
- Spring Boot is the automated tooling for Spring framework
  - it is a wrapper around spring
  - provides curated starter dependenicies
  - provides sensible "Auto-Configuration" based on classes found on class path
    - example if H2 is found, it will auto-configure and in memory database
  - provides externalised configuration via files and env variables
  - provides logging auto-configuration
  - provides performance metrics
  - provides healthcheck endpoints
  - provides enhanced failure information

## Spring Projects

1. Spring Data - collections of projects for persisting data to SQL and NoSQL databases
1. Spring Clould - tools for distributed systems
1. Spring Security - Authentication and Authorization
1. Spring Session - Distributed Web application session
1. Spring Integration - Enterprise Integration Patterns
1. Spring Batch - Batch processing
1. Spring State Machine - Open Source State Machine

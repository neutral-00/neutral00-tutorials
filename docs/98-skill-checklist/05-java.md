# Java Skill Checklist

Here are list of must have skillsets a senior Java Developer must have.
All these skills will be tested in a git repo: [https://github.com/neutral-00/poc-java](https://github.com/neutral-00/poc-java)
They will be group by branch name. For example, skills under `File and IO` will be tested under the git branch `file-and-io`.

## File and IO

### Text Files

1. [] Files.readString() with Path
2. [] Files.readAllLines() for line processing
3. [] BufferedReader with try-with-resources
4. [] Files.lines() stream for large files
5. [] Files.writeString() with StandardOpenOption
6. [] Files.write() with byte arrays
7. [] FileWriter with append mode
8. [] RandomAccessFile read/write position

### Excel (Apache POI)

9. [] XSSFWorkbook creation from file
10. [] read specific sheet by index/name
11. [] iterate rows with DataFormatter
12. [] get cell value by type (string/num)
13. [] create new XSSFWorkbook
14. [] add sheet with Sheet.createRow()
15. [] set cell styles (font, border)
16. [] write formulas (=SUM(A1:A10))
17. [] SXSSFWorkbook for streaming write

### PDF (PDFBox)

18. [] PDDocument.load() from file
19. [] PDFTextStripper text extraction
20. [] extract specific page range
21. [] PDDocument create new
22. [] add paragraphs with PDPageContentStream
23. [] create tables with coordinates
24. [] embed images in PDF

### CSV (OpenCSV)

25. [] CSVReader read all records
26. [] CSVReaderBuilder with custom separators
27. [] CSVWriter with quoting strategy
28. [] StatefulBeanToCsv for POJOs

### NIO.2

29. [] Files.walk() recursive directory
30. [] Files.find() with BiPredicate filter
31. [] Path.resolve() vs resolveSibling()
32. [] Files.isRegularFile() checks
33. [] Attributes read (size, lastModified)

### Serialization

34. [] ObjectOutputStream to file
35. [] transient field handling
36. [] ObjectInputStream readObject()
37. [] Externalizable custom serialization
38. [] Jackson ObjectMapper JSON
39. [] @JsonIgnore properties
40. [] polymorphic type handling

## Collections and Streams

### Core Streams

1. [] Stream.of() + filter() + map()
2. [] peek() for debugging
3. [] distinct() + sorted() + limit()
4. [] forEachOrdered() vs forEach()
5. [] flatMap() nested collections
6. [] Stream.generate() infinite streams

### Collectors

7. [] toList() vs toUnmodifiableList()
8. [] groupingBy() single level
9. [] groupingBy() with mapping()
10. [] partitioningBy() boolean split
11. [] joining() with delimiter/prefix
12. [] toMap() with mergeFunction
13. [] custom Collector.of()

### Concurrent Collections

14. [] ConcurrentHashMap.getOrDefault()
15. [] computeIfAbsent() thread-safe
16. [] CopyOnWriteArrayList add/remove
17. [] ConcurrentSkipListSet operations

### Optional & Specialized

18. [] Optional.ofNullable() chain
19. [] orElseGet() vs orElseThrow()
20. [] Optional.stream() processing
21. [] NavigableMap.floorEntry()
22. [] PriorityQueue poll/poll() with comparator

## Concurrency

### Threads & Executors

1. [] Thread.ofVirtual().start()
2. [] ExecutorService.newFixedThreadPool(4)
3. [] Executors.newVirtualThreadPerTaskExecutor()
4. [] Future.get() with timeout
5. [] shutdownNow() graceful shutdown

### CompletableFuture

6. [] supplyAsync() + thenApply()
7. [] thenCompose() for chaining
8. [] allOf() + anyOf() combinators
9. [] exceptionally() error handling
10. [] handleAsync() with Executor

### Locks & Synchronization

11. [] synchronized(this) vs intrinsic lock
12. [] ReentrantLock() with Condition
13. [] tryLock(1, TimeUnit.SECONDS)
14. [] ReadWriteLock read/write access
15. [] StampedLock optimistic read

### Atomics & Utilities

16. [] AtomicInteger.lazySet()
17. [] AtomicReference.compareAndSet()
18. [] ThreadLocal.withInitial()
19. [] Semaphore.acquireUninterruptibly()
20. [] CountDownLatch.await()
21. [] CyclicBarrier with action

## JVM Internals

### GC Tuning

1. [] -Xms -Xmx sizing
2. [] G1GC: -XX:MaxGCPauseMillis=200
3. [] ZGC: -XX:+UseZGC
4. [] Shenandoah GC flags

### Profiling

5. [] jcmd GC.run_finalization
6. [] JFR start with disk=true
7. [] VisualVM heap dump sampling
8. [] jstat -gcutil monitoring

### Diagnostics

9. [] -XX:+HeapDumpOnOutOfMemoryError
10. [] -XX:HeapDumpPath=/tmp/
11. [] jmap -histo:live
12. [] jstack thread dump

## Spring Boot

### REST APIs

1. [] @RestController with @RequestMapping
2. [] @GetMapping with produces/consumes
3. [] @PostMapping with @RequestBody
4. [] @PutMapping/@PatchMapping partial updates
5. [] @DeleteMapping with path variables
6. [] @RequestParam(required=false)
7. [] @PathVariable with regex patterns
8. [] @MatrixVariable in path segments
9. [] @RequestHeader authentication
10. [] @RequestPart multipart/form-data

### Validation

11. [] @Valid + @NotNull/@NotBlank
12. [] @Size + @Min/@Max constraints
13. [] @Pattern regex validation
14. [] @Email format validation
15. [] Custom @Validator implementation
16. [] Method validation @Valid on params
17. [] @Validated @ControllerAdvice

### Spring Security

18. [] SecurityFilterChain configuration
19. [] httpBasic() + httpBasicCustomizer()
20. [] formLogin() with custom login page
21. [] .authorizeHttpRequests() patterns
22. [] JWT filter with @PreAuthorize
23. [] OAuth2ResourceServer jwt()
24. [] PasswordEncoder BCrypt
25. [] UserDetailsService custom impl
26. [] CSRF disable for APIs

### Data JPA

27. [] @Entity @Table @Id @GeneratedValue
28. [] @Column(unique=true) constraints
29. [] JpaRepository custom methods
30. [] @Query native vs JPQL
31. [] @Query with @Param bindings
32. [] Specification predicate builder
33. [] Pageable + PageRequest.of()

### Caching

34. [] @EnableCaching + CaffeineCacheManager
35. [] @Cacheable(key="#id")
36. [] @CacheEvict(allEntries=true)
37. [] @CachePut conditional updates
38. [] CacheResolver custom logic

### Async Processing

39. [] @EnableAsync + @Async("taskExecutor")
40. [] TaskExecutor bean configuration
41. [] @Async CompletableFuture return
42. [] AsyncUncaughtExceptionHandler

### Configuration

43. [] @ConfigurationProperties(prefix="app")
44. [] @Value("${app.name}") injection
45. [] @Profile("dev") conditional beans
46. [] @ConditionalOnProperty flags
47. [] application.yml hierarchical config

### Actuator

48. [] /actuator/health customized
49. [] /actuator/metrics JVM metrics
50. [] /actuator/info git commit
51. [] /actuator/loggers dynamic levels
52. [] Micrometer Prometheus export

## Testing

### Unit Testing

1. [] @Test JUnit 5 assertions
2. [] @ParameterizedTest(valueSource)
3. [] @CsvSource test data
4. [] @TestMethodOrder(ORDERED)
5. [] @DisplayName descriptive names
6. [] @RepeatedTest(10) iterations
7. [] @Timeout(500ms) duration

### Mocking

8. [] @Mock @InjectMocks Mockito
9. [] @Spy partial mocking
10. [] BDDMockito given/willReturn
11. [] verify(times=1).method()
12. [] ArgumentCaptor capture args
13. [] @MockAnswer custom responses

### Spring Boot Tests

14. [] @SpringBootTest full context
15. [] @WebMvcTest controller slice
16. [] @DataJpaTest repository slice
17. [] @MockBean replace real beans
18. [] TestRestTemplate HTTP calls
19. [] MockMvc.post() chain + status()

### Integration Testing

20. [] @Testcontainers + PostgreSQLContainer
21. [] @Container Docker lifecycle
22. [] @DynamicPropertySource config
23. [] @Sql("test-data.sql") setup
24. [] @Sql(scripts={"cleanup.sql"})
25. [] @Transactional rollback default
26. [] Testcontainers Redis/Kafka

### Coverage

27. [] JaCoCo maven plugin config
28. [] jacoco:report aggregate
29. [] @Test coverage thresholds
30. [] sonar-project.properties

## Databases

### JPA Mappings

1. [] @OneToOne(cascade=CascadeType.ALL)
2. [] @OneToMany(mappedBy="parent")
3. [] @ManyToOne(fetch=LAZY)
4. [] @ManyToMany(fetch=EAGER)
5. [] @JoinColumn(name="user_id")
6. [] @JoinTable join table config
7. [] @Embedded vs @Embeddable
8. [] @ElementCollection collections

### Queries

9. [] JPQL SELECT u FROM User u
10. [] JOIN FETCH u.address
11. [] CriteriaQuery from EntityManager
12. [] CriteriaBuilder predicates
13. [] NativeQuery resultClass
14. [] @NamedQuery reusable queries

### Transactions

15. [] @Transactional(readOnly=true)
16. [] @Transactional(propagation=REQUIRES_NEW)
17. [] @Transactional(isolation=READ_COMMITTED)
18. [] TransactionTemplate programmatic
19. [] @Version optimistic locking
20. [] LockModeType.PESSIMISTIC_WRITE

### Migrations

21. [] Flyway baseline onUpdate
22. [] repeatable migrations R\_\_script
23. [] undo migrations U\_\_script
24. [] Liquibase changeset id

## Microservices

### Service Communication

1. [] @FeignClient(name="user-service")
2. [] @GetMapping with @PathVariable
3. [] Feign ErrorDecoder custom
4. [] @LoadBalanced RestTemplate
5. [] WebClient reactive HTTP calls
6. [] WebClient with exchangeStrategies
7. [] RestTemplate with interceptor

### Resilience

8. [] @CircuitBreaker(name="user")
9. [] @Retry(name="retry", fallbackMethod)
10. [] Resilience4j RateLimiter
11. [] Bulkhead concurrency limit
12. [] TimeLimiter timeout config
13. [] Custom Resilience4j config

### Service Discovery

14. [] @EnableDiscoveryClient Eureka
15. [] @EnableEurekaClient dedicated
16. [] eureka.client.serviceUrl
17. [] RestTemplate discovery enabled
18. [] Consul agent config basics

### Configuration

19. [] @EnableConfigClient bootstrap
20. [] spring.cloud.config.uri
21. [] {application}-{profile}.yml
22. [] RefreshScope @RefreshScope
23. [] @Value with config server

### Tracing & Monitoring

24. [] spring.sleuth.enabled tracing
25. [] Zipkin server connection
26. [] @NewSpan method tracing
27. [] @SpanTag custom tags
28. [] Micrometer distributed tracing
29. [] OpenTelemetry exporter

### Gateway

30. [] Spring Cloud Gateway routes
31. [] RouteLocator bean config
32. [] Predicate Path=/api/\*\*
33. [] Filter add-request-header
34. [] RateLimiter gateway filter
35. [] Hystrix fallbackUri

## Build and DevOps

### Maven

1. [] multi-module parent pom.xml
2. [] `<modules>` child declaration
3. [] dependencyManagement central
4. [] maven-enforcer-plugin rules
5. [] maven-shade-plugin uberjar
6. [] maven-surefire-plugin parallel
7. [] profiles for different envs

### Gradle

8. [] settings.gradle includeBuild
9. [] buildSrc custom plugins
10. [] gradle.properties JVM args
11. [] application plugin distTar
12. [] shadow plugin fat JAR
13. [] dependencyLocking lock files

### Docker

14. [] multi-stage Dockerfile build
15. [] FROM openjdk:21-jdk-slim
16. [] COPY target/\*.jar app.jar
17. [] ENTRYPOINT ["java","-jar"]
18. [] .dockerignore exclusions
19. [] HEALTHCHECK /actuator/health
20. [] EXPOSE 8080 networking

### CI/CD

21. [] GitHub Actions workflow yaml
22. [] matrix strategy versions
23. [] cache: maven m2/repository
24. [] setup-java action config
25. [] docker/build-push-action
26. [] deploy to Kubernetes

### Kubernetes

27. [] Deployment yaml replicas
28. [] Pod template spec containers
29. [] Service ClusterIP exposure
30. [] ConfigMap volumeMount
31. [] Secret base64 envFrom
32. [] HorizontalPodAutoscaler
33. [] Ingress nginx rules

## Design Patterns

### Creational

1. [] Enum singleton thread-safe
2. [] Abstract Factory interface
3. [] Factory Method override
4. [] Builder fluent interface
5. [] Prototype clone() method
6. [] @Builder(Lombok) annotation

### Structural

7. [] Adapter class composition
8. [] Decorator runtime wrapping
9. [] Proxy invocation handler
10. [] Composite tree structure
11. [] Facade simplified interface
12. [] Bridge separate abstraction

### Behavioral

13. [] Strategy functional interface
14. [] Observer @EventListener
15. [] Command encapsulated request
16. [] Iterator custom traversal
17. [] Template Method abstract
18. [] Chain of Responsibility filter
19. [] State object behavior
20. [] Visitor double dispatch

## Performance

### Profiling

1. [] @Benchmark JMH annotation
2. [] @Fork @Warmup @Measurement
3. [] @BenchmarkMode Mode.AverageTime
4. [] VisualVM CPU sampling
5. [] JProfiler live allocation
6. [] async-profiler flame graph

### Memory

7. [] Eclipse MAT leak suspects
8. [] OQL heap query language
9. [] jmap -histo histogram
10. [] -XX:+HeapDumpOnOutOfMemoryError
11. [] DirectByteBuffer off-heap

### Optimization

12. [] StringBuilder capacity
13. [] intern() string dedup
14. [] EnumSet bit operations
15. [] object pooling patterns
16. [] escape analysis -XX:+PrintEscape

## Security

### Authentication

1. [] SecurityFilterChain @Bean config
2. [] httpBasic(Customizer.withDefaults())
3. [] formLogin(loginPage="/login")
4. [] .logout().logoutUrl("/logout")
5. [] rememberMe(key="myapp")
6. [] UserDetailsService loadByUsername

### Authorization

7. [] @PreAuthorize("hasRole('ADMIN')")
8. [] @PostAuthorize("returnObject.owner == authentication.name")
9. [] MethodSecurityConfig enableMethodSecurity
10. [] .hasAuthority("SCOPE_read")
11. [] SpEL expressions in security
12. [] permissionEvaluator custom

### JWT/OAuth

13. [] JwtDecoder withSecretKey
14. [] OAuth2ResourceServer jwt()
15. [] NimbusJwtDecoder RS256
16. [] JwtAuthenticationConverter principalClaimName
17. [] opaqueToken introspection
18. [] clientCredentials grant type

### OWASP Protections

19. [] @RequestParam binding validation
20. [] Thymeleaf XSS autoescape
21. [] Content-Security-Policy header
22. [] Strict-Transport-Security
23. [] X-Frame-Options DENY
24. [] SQL injection @Param JPQL

## Reactive Programming

### Project Reactor

1. [] Mono.just("hello").subscribe()
2. [] Flux.range(1, 10).filter(n -> n % 2 == 0)
3. [] map() vs flatMap() distinction
4. [] zip(Flux1, Flux2) combine
5. [] merge() vs mergeSequential()
6. [] buffer() windowing chunks

### Operators

7. [] retry(3) exponential backoff
8. [] onErrorReturn("fallback")
9. [] doOnError logging
10. [] timeout(Duration.ofSeconds(5))
11. [] debounce(Duration.ofMillis(300))
12. [] distinctUntilChanged()

### Spring WebFlux

13. [] @EnableWebFlux functional
14. [] RouterFunctions.route()
15. [] RouterFunction GET("/users")
16. [] HandlerFunction with ServerResponse
17. [] WebFlux.fn handler methods
18. [] RSocketRequester messaging

## Java 21 Features

### Records

1. [] `public record Point(int x, int y) {}`
2. [] record with compact constructor
3. [] record canonical constructor
4. [] @Value record immutability
5. [] record toString() auto
6. [] record equals() hashCode()

### Pattern Matching

7. [] instanceof String s checks
8. [] `switch (obj) { case Integer i -> ... }`
9. [] sealed interface Shape permits Circle, Rectangle
10. [] case Circle c -> c.radius()
11. [] case null, default -> throw

### Virtual Threads

12. [] Thread.ofVirtual().start(runnable)
13. [] Executors.newVirtualThreadPerTaskExecutor()
14. [] StructuredTaskScope.of().fork(task)
15. [] ScopedValue allocation context
16. [] ThreadOfVirtual pinning avoidance

### Other Features

17. [] text blocks """ multiline """
18. [] String.isBlank() stripIndent()
19. [] Sequence of var i for (var i : list)
20. [] Record patterns deconstruction
21. [] switch preview features

## Logging

### SLF4J/Logback

1. [] @Slf4j Lombok annotation
2. [] `log.info("User: {}", userId)`
3. [] MDC.put("requestId", id)
4. [] logback-spring.xml profiles
5. [] rollingPolicy time/size

### Advanced

6. [] AsyncAppender logback
7. [] Sentry integration
8. [] Fluentd forwarder
9. [] log4j2 JUL bridge

## Messaging

### Kafka

1. [] KafkaTemplate send(topic, key, value)
2. [] @KafkaListener(topics="orders")
3. [] ConsumerRebalanceListener
4. [] KafkaTransactionManager

### RabbitMQ

5. [] @RabbitListener(queues="queue1")
6. [] RabbitTemplate convertSend
7. [] DirectExchange routing
8. [] TopicExchange wildcards

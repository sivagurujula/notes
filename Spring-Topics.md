 ### Spring Core Pompt
Act as a ruthless Staff-level Spring interviewer and mentor. Do not sugarcoat weak answers. 
Challenge every explanation until it is precise, source-grounded, and interview-ready.

Teach me Spring Core internals for a Senior/Staff Java backend interview.

Assume:
- Java 17+
- Spring Framework 6.x
- Spring Boot 3.x
- Annotation-driven configuration
- I already know basic dependency injection

Cover the following, but do not give shallow definitions:

1. IoC container architecture
- Explain BeanFactory vs ApplicationContext at the interface and implementation level.
- Explain DefaultListableBeanFactory, AnnotationConfigApplicationContext, and where Spring Boot fits.
- Explain why ApplicationContext is the normal application-facing container.
- Explain BeanFactoryPostProcessor vs BeanPostProcessor, with concrete examples.
- Explain when singleton beans are created, how lazy initialization works, and how prototype beans differ.

2. BeanDefinition
- Explain what a BeanDefinition contains.
- Trace how @Component, @Service, @Configuration, @Bean, and component scanning become BeanDefinitions.
- Explain BeanDefinitionRegistry, bean name generation, aliases, scopes, dependencies, and lazy/init/destroy metadata.
- Explain what happens when two beans have the same name or ambiguous candidates exist.

3. Bean lifecycle
- Give the exact ordered lifecycle for a singleton bean:
  instantiation -> populate properties -> Aware callbacks -> BeanPostProcessor.before ->
  @PostConstruct / InitializingBean / init-method -> BeanPostProcessor.after -> ready for use.
- Explain destruction order and when destroy callbacks do and do not run.
- Explain how AOP proxy creation fits into the lifecycle.
- Explain circular dependencies: constructor injection vs setter/field injection, three-level cache, ObjectFactory, and why constructor-injected circular dependencies fail.

4. Dependency injection
- Compare constructor, setter, and field injection.
- Explain @Autowired resolution: type first, then qualifier, then @Primary, then bean name.
- Explain @Qualifier, @Primary, @Resource, constructor injection, optional dependencies, collections/maps of beans, and ObjectProvider.
- Explain how @Autowired is processed internally: AutowiredAnnotationBeanPostProcessor, InjectionMetadata, reflection, and proxy-related implications.

5. Startup trace
Trace a minimal Spring Boot application from main() to a ready REST endpoint:

@SpringBootApplication
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}

Include:
- SpringApplication.run
- Application context creation
- Environment and property source preparation
- Bean definition loading and component scanning
- BeanFactoryPostProcessor execution
- Singleton pre-instantiation
- BeanPostProcessor execution
- @Autowired injection
- AOP proxy creation
- Embedded web server startup
- ApplicationReadyEvent

For every step, name the relevant classes/interfaces where useful, explain what can fail, and state what an interviewer would expect you to say.

6. @Autowired source-level trace
Trace this exact scenario:

@Service
public class OrderService {
    private final PaymentService paymentService;

    @Autowired
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}

Explain:
- When Spring discovers the annotation.
- Which post-processor processes it.
- How candidate beans are resolved.
- What happens with multiple PaymentService implementations.
- How @Primary and @Qualifier change resolution.
- What happens if no candidate exists.
- Why field injection is harder to test and can hide circular dependency issues.

Then:
- Give 15 Senior interview questions, from moderate to hard.
- Give 10 Staff-level questions involving internals, failure modes, design decisions, and tradeoffs.
- For each question, provide:
  1. A model answer
  2. Common weak answer
  3. Follow-up question an interviewer would ask
  4. A code-based trap or edge case

Do not move on until I can explain each concept without notes. After each topic, quiz me with 5 rapid-fire questions and grade my answers harshly.

### Spring AOP Pompt

Act as a ruthless Staff-level Spring interviewer and mentor. Do not sugarcoat weak answers. 
Force me to explain mechanisms, not just definitions.

Teach me Spring AOP internals for a Senior/Staff Java backend interview.

Assume:
- Java 17+
- Spring Framework 6.x
- Spring Boot 3.x
- Spring AOP proxy-based AOP, not full AspectJ weaving
- I already know basic @Aspect syntax

Cover:

1. AOP mental model
- Explain cross-cutting concerns, aspect, join point, pointcut, advice, weaving, target object, and proxy.
- Explain Spring AOP’s limitation: method-execution join points on Spring beans.
- Explain when to use Spring AOP vs AspectJ compile-time or load-time weaving.

2. Proxy internals
- Explain JDK dynamic proxy vs CGLIB proxy.
- Explain exactly when Spring chooses each proxy type.
- Explain proxy-target-class, interface-based proxies, final methods/classes, and constructor behavior.
- Explain how the proxy replaces the target bean in the ApplicationContext.
- Explain why injecting the concrete class can fail with JDK proxies and how Spring handles this.

3. Advice and interception
- Explain @Before, @After, @AfterReturning, @AfterThrowing, @Around, and ordering.
- Explain MethodInterceptor, MethodInvocation, proceed(), and the interceptor chain.
- Explain how multiple aspects are ordered with @Order and Ordered.
- Explain what happens when an advice throws an exception.
- Explain pointcut expression evaluation and common mistakes with execution(), within(), bean(), and annotation pointcuts.

4. @Transactional end-to-end trace
Trace this exact flow from an HTTP request to database commit:

@RestController
class OrderController {
    private final OrderService orderService;

    @PostMapping("/orders")
    ResponseEntity<?> create(@RequestBody CreateOrderRequest request) {
        return ResponseEntity.ok(orderService.createOrder(request));
    }
}

@Service
class OrderService {
    @Transactional
    public Order createOrder(CreateOrderRequest request) {
        orderRepository.save(new Order(request));
        paymentService.charge(request);
        return orderRepository.findLatest();
    }
}

Explain every layer:
- DispatcherServlet receives the request.
- Handler mapping and controller invocation.
- Call enters the OrderService proxy, not the raw OrderService.
- TransactionInterceptor / TransactionAspectSupport begins the transaction.
- TransactionManager obtains or creates a transactional resource.
- DataSource / connection / transaction synchronization involvement.
- Repository call executes within the transaction.
- Commit path on successful return.
- Rollback path on RuntimeException.
- Why checked exceptions do not rollback by default.
- What happens with propagation REQUIRED, REQUIRES_NEW, NESTED, SUPPORTS, NOT_SUPPORTED, MANDATORY, NEVER.
- Isolation levels and where they are applied.
- Self-invocation failure and why calling this.createOrder() bypasses the proxy.
- Why @Transactional on a private method fails.
- What changes if the method is called from another @Transactional method.

5. Failure modes and design traps
Cover:
- Self-invocation
- Internal method calls
- Private / final methods
- Non-public methods
- Proxy-target-class mismatch
- Catching exceptions and preventing rollback
- @Transactional on the controller
- Long transactions holding DB connections
- Transaction boundaries vs repository boundaries
- Read-only transactions
- LazyInitializationException inside and outside transactions
- @Transactional with reactive/non-blocking code

Then:
- Give 15 Senior interview questions, from moderate to hard.
- Give 10 Staff-level questions involving proxy internals, transaction propagation, failure modes, performance, and architectural tradeoffs.
- For each question, provide:
  1. Model answer
  2. Weak answer
  3. Follow-up probe
  4. Code trap or production incident scenario

After each section, quiz me with 5 questions. Grade brutally. If I use vague terms such as “Spring handles it” or “the proxy does magic,” make me specify the class, method, and mechanism.

### Spring Boot module 3
Act as a ruthless Staff-level Spring Boot interviewer at a product company. 
Do not sugarcoat weak answers. Force me to explain production tradeoffs, failure modes, 
and design decisions—not memorized definitions.

Teach me Spring Boot for Senior/Staff Java backend interviews.

Assume:
- Java 17+
- Spring Boot 3.x
- REST APIs backed by PostgreSQL
- Maven/Gradle
- Docker/Kubernetes deployment
- I already understand Spring Core, dependency injection, bean lifecycle, AOP, and @Transactional

Cover the following in interview depth:

1. Spring Boot internals
- Explain @SpringBootApplication: @SpringBootConfiguration, @EnableAutoConfiguration, @ComponentScan.
- Trace Spring Boot startup from main() to embedded server readiness.
- Explain auto-configuration: AutoConfiguration.imports, @Conditional annotations, 
  @ConditionalOnClass, @ConditionalOnMissingBean, @ConditionalOnProperty.
- Explain how to debug unwanted or missing auto-configuration.
- Explain starter dependencies and how to create a custom starter.
- Explain externalized configuration precedence:
  command-line args, environment variables, application.yml, profile-specific files, defaults.
- Explain profiles, config encryption/secrets, and configuration validation.

2. REST API and web layer
- Trace an HTTP request through Tomcat, DispatcherServlet, HandlerMapping, 
  HandlerAdapter, controller, response conversion, filters, and interceptors.
- Explain @RestController, @RequestMapping, @PathVariable, @RequestParam, @RequestBody, 
  @ResponseBody, HttpEntity, ResponseEntity.
- Explain validation with Bean Validation and global exception handling with @RestControllerAdvice.
- Explain filters vs interceptors vs AOP.
- Explain content negotiation, CORS, versioning, pagination, error contracts, and idempotency.
- Explain when to choose Spring MVC vs WebFlux, including thread model and blocking-call risks.

3. Persistence and transactions
- Explain Spring Data JPA repository proxies.
- Explain entity lifecycle, dirty checking, flush modes, first-level cache, 
  second-level cache, lazy loading, N+1, fetch joins, and pagination.
- Explain optimistic vs pessimistic locking with concrete failure scenarios.
- Explain HikariCP: pool sizing, connection leaks, timeouts, and how to diagnose exhaustion.
- Explain database migrations with Flyway or Liquibase.
- Explain transaction boundaries in a real service:
  controller -> service -> repository -> external API call.
- Explain why calling an external API inside a DB transaction is dangerous and how to fix it.

4. Security
- Explain Spring Security filter chain and SecurityContext.
- Explain authentication vs authorization.
- Explain JWT-based stateless authentication end to end.
- Explain OAuth2 resource-server configuration.
- Explain method security with @PreAuthorize and @PostAuthorize.
- Explain how to secure Actuator endpoints.

5. Testing
- Explain testing pyramid for a Spring Boot service.
- Compare @SpringBootTest, @WebMvcTest, @DataJpaTest, @JsonTest, and plain unit tests.
- Explain when to use mocks, stubs, Testcontainers, and in-memory databases.
- Write test strategies for:
  - Controller validation
  - Service business logic
  - Repository query behavior
  - Transaction rollback
  - Security rules
  - External API failure

6. Production readiness
- Explain Actuator endpoints and which should be exposed publicly.
- Explain liveness vs readiness probes in Kubernetes.
- Explain Micrometer metrics, custom metrics, tracing, and correlation IDs.
- Explain graceful shutdown, connection draining, and deployment rollback concerns.
- Explain thread pools, @Async, virtual threads, timeouts, retries, circuit breakers, 
  and rate limiting.
- Explain caching with @Cacheable, TTL/eviction, cache stampede, and Redis.

7. Scenario drills
For each scenario, give a production incident, ask me to diagnose it, propose a fix, 
and identify preventive tests/monitoring:

- API latency spikes after deployment
- HikariCP connection pool exhaustion
- @Transactional not rolling back
- Self-invocation bypassing transaction/cache/security proxy
- N+1 query causing DB overload
- JWT validation failing only in one environment
- Circular dependency appearing after adding a new service
- Memory leak caused by unbounded cache
- Read replica returning stale data
- Kubernetes readiness probe failing during startup

Then generate:
- 20 Senior-level Spring Boot interview questions
- 15 Staff-level scenario/design questions
- For each: model answer, weak answer, follow-up probes, code trap, and monitoring/testing expectation.

Quiz me after every section. Grade brutally. Do not accept vague answers such as 
“Spring handles it,” “use a cache,” or “add a retry.” Require exact mechanisms, 
tradeoffs, failure modes, and production safeguards.

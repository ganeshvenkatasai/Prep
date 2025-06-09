# Core Concepts  
- Spring Boot: Framework for creating stand-alone, production-grade Spring apps with minimal configuration.  
- Auto-Configuration: Automatically configures Spring apps based on dependencies in the classpath.  
- Starter POMs: Predefined dependency descriptors to simplify Maven/Gradle configurations.  
- Spring Initializr: Web-based tool to bootstrap Spring Boot projects with required dependencies.  
- @SpringBootApplication: Combines @Configuration, @EnableAutoConfiguration, and @ComponentScan.  

# Dependency Injection & Beans  
- @Component: Marks a class as a Spring-managed bean.  
- @Service: Specialized @Component for service-layer beans.  
- @Repository: Specialized @Component for DAO/Repository classes.  
- @Autowired: Injects dependencies automatically (field, constructor, or setter).  
- @Qualifier: Resolves ambiguity when multiple beans of the same type exist.  
- @Primary: Indicates a preferred bean when multiple candidates exist.  

# Web & REST  
- @RestController: Combines @Controller and @ResponseBody for REST APIs.  
- @RequestMapping: Maps HTTP requests to handler methods (can be narrowed with @GetMapping, @PostMapping, etc.).  
- @PathVariable: Extracts values from URI templates.  
- @RequestParam: Binds query parameters to method arguments.  
- @RequestBody: Maps HTTP request body to a Java object (deserialization).  
- @ResponseBody: Serializes return objects into HTTP response body (JSON/XML).  
- @ResponseStatus: Customizes HTTP response status code.  

# Data Access  
- Spring Data JPA: Simplifies database access using JPA repositories.  
- JpaRepository: Interface providing CRUD operations for JPA entities.  
- @Entity: Marks a class as a JPA entity (maps to a database table).  
- @Id: Specifies the primary key of an entity.  
- @GeneratedValue: Configures auto-generation of primary keys.  
- Hibernate: Default JPA implementation used by Spring Boot.  

# Database & Transactions  
- @Transactional: Defines transaction boundaries (ACID properties).  
- Spring JDBC: Simplifies JDBC operations using JdbcTemplate.  
- Flyway/Liquibase: Database migration tools for versioning schema changes.  

# Security  
- Spring Security: Framework for authentication and authorization.  
- OAuth2: Protocol for delegated authorization (social logins).  
- JWT (JSON Web Token): Stateless token-based authentication.  
- @PreAuthorize: Method-level security (e.g., @PreAuthorize("hasRole('ADMIN')")).  

# Exception Handling  
- @ControllerAdvice: Global exception handling for controllers.  
- @ExceptionHandler: Handles exceptions at the controller level.  
- ResponseEntityExceptionHandler: Base class for custom exception handling.  

# Testing  
- @SpringBootTest: Bootstraps entire application context for integration tests.  
- @WebMvcTest: Tests only the web layer (controllers).  
- @DataJpaTest: Tests JPA repositories with an embedded database.  
- MockMvc: Mocks HTTP requests for controller testing.  
- @MockBean: Adds mock objects to the Spring context.  

# Actuator & Monitoring  
- Spring Boot Actuator: Provides production-ready monitoring endpoints.  
- /health: Checks application health (DB, disk space, etc.).  
- /metrics: Exposes application metrics (memory, threads, etc.).  
- @EnableAdminServer: Enables Spring Boot Admin dashboard.  

# Caching  
- @EnableCaching: Enables Spring’s caching abstraction.  
- @Cacheable: Caches method results (e.g., @Cacheable("users")).  
- @CacheEvict: Removes entries from cache (e.g., after update).  

# Logging  
- SLF4J: Abstraction layer for logging (default: Logback).  
- Lombok @Slf4j: Simplifies logging with Lombok.  

# Async & Scheduling  
- @Async: Executes methods asynchronously.  
- @EnableAsync: Enables async method execution.  
- @Scheduled: Runs methods periodically (e.g., @Scheduled(fixedRate=5000)).  

# Microservices  
- Spring Cloud: Tools for building microservices (config server, service discovery, etc.).  
- Eureka: Service registry for dynamic service discovery.  
- Zuul/Spring Cloud Gateway: API gateway for routing requests.  
- Hystrix: Circuit breaker for fault tolerance.  

# Docker & Deployment  
- Dockerfile: Defines containerization steps for Spring Boot apps.  
- JAR vs WAR: Spring Boot defaults to embedded server (JAR).  
- Kubernetes: Orchestration tool for deploying Spring Boot apps at scale.  

# Best Practices  
- YAML over Properties: More readable configuration.  
- Profile-specific config: application-{profile}.yml for environment-specific settings.  
- DTO over Entities: Use DTOs for API responses to avoid exposing internal models.  

## Java

```

```





## Spring Boot

```
1. Difference between Spring and Spring Boot

Spring: A framework for Java EE development, requires manual configuration.
Spring Boot: Built on Spring, provides auto-configuration, embedded servers, and starter dependencies for rapid development.

2. What are the advantages of Spring Boot over Spring?

No XML configuration (uses annotations & application.properties).
Faster setup with spring-boot-starter dependencies.
Embedded servers (no need for external deployment).
Auto-configuration (e.g., DataSource, JPA).
Actuator for monitoring and management.

3. What is the use of @SpringBootApplication?

It combines three annotations:
@Configuration → Marks the class as a config source.
@EnableAutoConfiguration → Enables auto-setup of beans.
@ComponentScan → Scans for @Component, @Service, etc., in the package.

4. How does Spring Boot handle database configuration?

Define connection details in application.properties:

spring.datasource.url=jdbc:mysql://localhost:3306/db  
spring.datasource.username=root  
spring.datasource.password=123  

Spring Boot auto-configures DataSource, JdbcTemplate, and Hibernate.

5. What is the difference between @RestController and @Controller?

@Controller :
Used for MVC (returns view names like "home.html").
Requires @ResponseBody to return data.

@RestController
Used for REST APIs (returns JSON/XML).
Includes @ResponseBody by default.

6. What is Spring Boot Actuator?

A module providing production-ready endpoints for monitoring:
/health → Application status.
/metrics → Performance stats.
/info → Custom app details.
/beans → Lists all Spring beans.

7. How do you change the embedded server in Spring Boot?

Exclude Tomcat and add Jetty/Undertow in pom.xml:

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

8. What is Dependency Injection (DI) in Spring?

A design pattern where dependencies are injected (not created by the class).

9. What is @Autowired used for?

Automatically injects dependencies (beans) into a class.
Works on constructors, setters, or fields.

10. What is the difference between @Component, @Service, and @Repository?

All are stereotypes (specialized @Component):
@Component → Generic Spring-managed bean.
@Service → Business logic layer.
@Repository → Data access layer (auto-translates DB exceptions).

11. How do you handle exceptions in Spring Boot?

@ExceptionHandler(UserNotFoundException.class)  
public ResponseEntity<String> handleError(UserNotFoundException ex) {  
    return ResponseEntity.status(404).body(ex.getMessage());  
}  

@ControllerAdvice  
public class GlobalExceptionHandler { ... }

13. How do you connect to multiple databases in Spring Boot?

Define multiple DataSource beans with @Configuration.

Use @Primary for the main DB.

Specify configs in application.properties:

properties
# Primary DB  
spring.datasource.url=jdbc:mysql://localhost/db1  

# Secondary DB  
spring.second-datasource.url=jdbc:postgresql://localhost/db2  

14. What is the role of DispatcherServlet?

Front controller in Spring MVC.

Routes requests to controllers, manages view resolution, and handles exceptions.

Workflow:

text
HTTP Request → DispatcherServlet → Controller → Service → DB → Response  

15. How do you implement security in Spring Boot?

Use Spring Security:

Add dependency:

<dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-security</artifactId>  
</dependency>  
Configure SecurityConfig:

@Configuration  
@EnableWebSecurity  
public class SecurityConfig {  
    @Bean  
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {  
        http.authorizeRequests().anyRequest().authenticated().and().httpBasic();  
        return http.build();  
    }  
}  


```

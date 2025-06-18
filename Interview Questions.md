## Java

```
Static Method: Belongs to the class (no instance needed).
Instance Method: Requires an object.

Feature	  	Stack Memory	  			Heap Memory
Stores	  	Primitives, method calls, references	Objects, arrays, instance variables
Lifetime  	Short-lived (method scope)		Long-lived (until garbage collected)
Thread    	Safety	Each thread has its own stack	Shared among all threads
Speed	  	Faster access				Slower access
Memory Mgmt.	Automatic (LIFO)			Managed by Garbage Collector (GC)
Size		Fixed (can overflow)			Dynamic (can run out of memory)

Wrapper Classes (Integer, Double): Used in collections (e.g., List<Integer>). Provide utility methods (Integer.parseInt()).
Primitives (int, double): Better performance.

Array for performance-critical fixed-size data.
List for flexibility.

Set (HashSet, TreeSet) : No duplicates. Unordered (except TreeSet).
List (ArrayList, LinkedList) Allows duplicates. Ordered (index-based).

1. Comparable (java.lang.Comparable)
Purpose: Defines the natural ordering of a class (default sorting logic).
Method to Implement: compareTo(T obj)

class Student implements Comparable<Student> {
    String name;
    int age;

    @Override
    public int compareTo(Student other) {
        return this.age - other.age; // Sort by age (ascending)
    }
}

// Usage:
List<Student> students = new ArrayList<>();
students.add(new Student("Alice", 25));
students.add(new Student("Bob", 20));
Collections.sort(students); // Sorts by age (natural order)


2. Comparator (java.util.Comparator)
Purpose: Provides custom sorting logic without modifying the original class.

Method to Implement: compare(T obj1, T obj2)
// Comparator for sorting by name
class NameComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.name.compareTo(s2.name); // Sort by name (String's natural order)
    }
}

// Usage:
List<Student> students = new ArrayList<>();
students.add(new Student("Alice", 25));
students.add(new Student("Bob", 20));
Collections.sort(students, new NameComparator()); // Sorts by name

Using Lambda (Java 8+)
// Sort by age (descending)
Collections.sort(students, (s1, s2) -> s2.age - s1.age);

// Alternative (using Comparator.comparing)
students.sort(Comparator.comparing(Student::getName)); // Sort by name
students.sort(Comparator.comparingInt(Student::getAge).reversed()); // Sort by age (descending)


Interface						Abstract Class
All methods are abstract (Java 8+ allows default).	Can have abstract + concrete methods.
Supports multiple inheritance.				Single inheritance.
No constructors.					Can have constructors.

Final:
Variables: Cannot be reassigned (final int x = 5;).
Methods: Cannot be overridden.
Classes: Cannot be inherited.

== vs equals()
==: Compares memory addresses (references).
equals(): Compares content (overridden in String, Integer).

Integer a = 5;    // Autoboxing  
int b = a;        // Unboxing  

Checked Exceptions		Unchecked Exceptions
Compile-time (must handle).	Runtime (optional handling).
E.g., IOException.		E.g., NullPointerException.

StringBuilder for single-threaded apps.
StringBuffer for multithreading.

Synchronized Method: Locks the entire object : public synchronized void myMethod() { ... } 
Synchronized Block: Locks a specific section : synchronized(this) { ... }

Overloading					Overriding
Same method name, different parameters.		Same method signature in subclass.
Compile-time polymorphism.			Runtime polymorphism.

Serialization: Object → Byte stream (for storage/transfer) : ObjectOutputStream.writeObject(obj); // Serialize  
Deserialization: Byte stream → Object : ObjectInputStream.readObject();     // Deserialize  

ArrayList for frequent reads.
LinkedList for frequent modifications.

HashMap				HashTable
Not thread-safe.		Thread-safe (synchronized).
Allows null keys/values.	No null keys/values.

Best Practice: Prefer HashMap (use ConcurrentHashMap for threads).

Enum: Type-safe, can have methods.

Garbage Collection: Automatic (Java, Python). GC prevents memory leaks but adds overhead.
Manual Management: Explicit malloc/free (C/C++).



It works : return n % 2 == 0 ? n : n * 2;

Type casting : (int)


Functional      		OOP Programming
Pure functions, immutability.	Objects, state, inheritance.
E.g., Java Streams.		E.g., Java classes.
Key Difference: FP avoids side effects; OOP models real-world entities.


Shallow Copy: Copies references (shared nested objects).    ArrayList<String> shallow = original; 
Deep Copy: Copies entire object hierarchy.		    ArrayList<String> deep = new ArrayList<>(original);  


Java is always pass-by-value.		
For primitives: A copy of the value is passed.
For objects: A copy of the reference (memory address) is passed.

Thread vs Runnable
Thread: A class. Extending it limits flexibility (Java doesn’t support multiple inheritance).
Runnable: An interface. Preferred because:
Allows extending another class.
Better for thread pooling.


Switch : alternative to long if-else-if
Without break, execution will "fall through" to the next case.
default case: Optional but recommended for handling unexpected values.
duplicate case not allowed, comiplation error
Arrows syntax can also be used
Arrow and : syntax both cant be used
switch can return values
Using null in a switch statement will throw a NullPointerException.


String str = Integer.toString(number);
String str = String.valueOf(number);
String str = "" + number;

int number = Integer.parseInt(str);
Integer number = Integer.valueOf(str); 

class path : where the jar class files are located


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


@Autowired vs @Qualifier
@Autowired: Injects a bean by type.
@Qualifier: Injects a specific bean by name.





```

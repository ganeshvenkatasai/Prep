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

Singleton Design Pattern : private constructor, synchronized method :  public static synchronized ThreadSafeSingleton getInstance()

Integer can store null, where int cant store null

int to String ->  String.valueOf(int) or Integer.toString(int)
String to int -> Integer.valueOf(String) or Integer.parseInt(String)

HashMap (Collision -> Linkedlist before java8, Red Black Tree after java 8)
TreeMap -> Red Black Tree

Intermediate Operations (Lazy Evaluation) -> These operations return a new stream and only execute when a terminal operation is called.

it is not possible to use two terminal operations one after another on the same Java Stream.

.flatMap(List::stream) 

List<Integer> squaredNumbers = numbers.stream()
    .peek(n -> System.out.println("Before map: " + n))
    .map(n -> n * n)
    .peek(n -> System.out.println("After map: " + n))
    .collect(Collectors.toList());
    
    
List<String> names = List.of("Alice", "Bob", "Charlie");

Set<String> nameSet = names.stream()
    .collect(Collectors.toSet());  // Convert to Set



import java.util.Scanner;
Scanner scanner = new Scanner(System.in);
String name = scanner.nextLine();

next() - Reads a single word (until whitespace)
nextLine() - Reads an entire line (until newline)
nextInt(), nextDouble(), nextBoolean()

// Always close the scanner when done
   scanner.close();

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class FileWriteBuffered {
    public static void main(String[] args) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"))) {
            writer.write("Using BufferedWriter");
            writer.newLine();
            writer.write("More efficient for multiple writes");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileReadBuffered {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("input.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}


ExecutorService: java.util.concurrent // from Java 5 onward
ExecutorService executor = Executors.newFixedThreadPool(4); // 4 threads
ExecutorService executor = Executors.newCachedThreadPool();
ExecutorService executor = Executors.newSingleThreadExecutor();
ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(2);

// execute() :
executor.execute(() -> {
    System.out.println("Task running in thread: " + Thread.currentThread().getName());
});

executor.shutdown(); // Shutdown when done

// submit() :
Future<Integer> future = executor.submit(() -> {
    Thread.sleep(1000);
    return 42; // Returns a result
});

try {
    System.out.println("Result: " + future.get()); // Blocks until result is available
} catch (Exception e) {
    e.printStackTrace();
}

executor.shutdown();


Atomic Variables :
AtomicInteger (for int)
AtomicLong (for long)
AtomicBoolean (for boolean)
AtomicReference<T> (for any object)
AtomicIntegerArray, AtomicLongArray (for arrays)

AtomicInteger counter = new AtomicInteger(0);
counter.set(10); // Sets value to 10
int value = counter.get(); // Reads value (10)
boolean success = counter.compareAndSet(10, 20); // If current value is 10, set to 20
System.out.println(counter.incrementAndGet()); // 1 (++i)
System.out.println(counter.getAndIncrement()); // 1 (i++)
AtomicInteger counter = new AtomicInteger(5);
counter.updateAndGet(x -> x * 2); // 10
counter.accumulateAndGet(3, (x, y) -> x + y); // 13


Multithreading :
Thread.currentThread().getName() // Thread-0

New: When created but not started
Runnable: When start() is called
Running: When executing
Blocked/Waiting: When waiting for resources
Terminated: When execution completes

 t1.join(); // Wait for t1 to finish


Most collections throw ConcurrentModificationException if modified during iteration.
Use Iterator.remove() for safe removal in List, Set, Map, Queue, Deque.
Java 8+? Prefer removeIf() where possible.
Concurrent collections (ConcurrentHashMap, CopyOnWriteArrayList) allow direct removal but



The default initial capacity of an ArrayList in Java is 10.
The growth factor is (oldCapacity * 3)/2 + 1
If created with new ArrayList<>(0), Java delays allocation until the first element is added.
If you know the approximate size, initialize with a higher capacity to avoid reallocations

The load factor is a critical performance parameter in hash-based collections (HashMap, HashSet, LinkedHashMap, HashTable)
Default HashMap (Capacity=16, Load Factor=0.75)
Map<String, Integer> map = new HashMap<>(16, 0.5f); // Resizes at 8 elements


Collections.synchronizedMap() (Legacy Thread-Safe Map) :
Wraps any Map (e.g., HashMap, LinkedHashMap) and makes it thread-safe.
Uses synchronized blocks on the entire map (monitor lock)

Map<String, Integer> map = new HashMap<>();
Map<String, Integer> syncMap = Collections.synchronizedMap(map); // Now thread-safe

Poor performance under high contention (only one thread can access the map at a time).

ConcurrentHashMap (Modern Thread-Safe Map) :
Uses fine-grained locking (lock striping) and CAS (Compare-And-Swap) operations.
Allows multiple threads to read and write concurrently without full synchronization.

Map<String, Integer> concurrentMap = new ConcurrentHashMap<>();

Higher throughput in multi-threaded environments.
Atomic operations (e.g., putIfAbsent(), compute()).
Scalable (better than synchronizedMap).
Does not allow null keys/values (throws NullPointerException)


ThreadLocal:
Each thread has its own instance of the variable.
No synchronization needed (since threads don’t share the variable).
Common use cases:
Storing user sessions (e.g., in web apps).
Storing transaction contexts (e.g., in JDBC).
Per-thread caching (e.g., SimpleDateFormat).

ThreadLocal<Integer> threadLocalCounter = new ThreadLocal<>();
// Each thread sets its own value
threadLocalCounter.set(0);
// Each thread increments its own copy
threadLocalCounter.set(threadLocalCounter.get() + 1);

Always threadLocal.remove() after use to prevent memory leaks



HashMap -> one null key and multiple null values : 0 index is reserved for null key


Thread-Safe Classes in Java:
Hashtable
Vector
Stack
Collections.synchronizedList(List<T> list)
Collections.synchronizedMap(Map<K,V> map)
Collections.synchronizedSet(Set<T> set)
ConcurrentHashMap	High-concurrency Map	Fine-grained locking, atomic operations (putIfAbsent, compute)
CopyOnWriteArrayList	Thread-safe List	Snapshot iteration (no ConcurrentModificationException)
CopyOnWriteArraySet	Thread-safe Set	Backed by CopyOnWriteArrayList
BlockingQueue	        Thread-safe FIFO queue	Supports producer-consumer patterns
ConcurrentLinkedQueue	Lock-free thread-safe queue	Non-blocking, high performance
ConcurrentSkipListMap	Thread-safe sorted Map	Scalable alternative to TreeMap
ConcurrentSkipListSet	Thread-safe sorted Set	Backed by ConcurrentSkipListMap





```





## Spring Boot

```

Dependency Injection :
1. Constructor Injection
2. Setter Injection
3. Autowired

Constructor Injection is preferred over Setter injection:
when a class cannot function without its dependencies
When you want dependencies to be immutable 

What are Spring Beans?
Spring Beans are objects that form the backbone of a Spring application
Managed by the Spring IoC container
Instantiated, assembled, and managed by the Spring framework

Lifecycle Management: Spring handles creation, initialization, and destruction
Dependency Injection: Beans can receive other beans they depend on
Scope Control: Beans can have different lifecycles (singleton, prototype, etc.)
Configuration: Can be defined via XML, annotations, or Java configuration

Example :
Spring starts up
Creates UserService bean
Injects UserRepository into it
Calls @PostConstruct setup method
Your app uses UserService for months
On shutdown, Spring calls @PreDestroy cleanup

@SpringBootApplication : Start of application
@Configuration : 
@EnableAutoConfiguration : automatically sets up database connections
@ComponentScan : finds and registers your @Service, @Repository, and @Controller

@Profile : differentiate between dev and prod environments

Method-Level @Transactional is better (if all methods in class needs transactions then use class level Transactional)
For read-only operations, always specify: 
@Transactional(readOnly = true)
public Order getOrder(Long id) { ... }

When you apply @Transactional at both the class and method level in Spring, the method-level annotation takes precedence over the class-level (it leads to unusual behaviour)

Compensating Transaction / Distrubuted Transaction Pattern : Saga (it is used in Remote Service failing)

How Spring Boot Simplifies Web Development
Auto-configuration: Detects your classpath and automatically configures beans
Embedded Servers: Runs Tomcat, Jetty, or Undertow directly (no WAR deployment needed)
Annotations-based controllers with no boilerplate
Auto JSON conversion
Actuator	Ready-made health checks, metrics, monitoring
Security Starter	Add auth with spring-boot-starter-security
Externalized Config	Switch between dev/prod with profiles
Automatic DataSource setup (just define properties)
Spring Data JPA reduces repository code by 80%
Dependency Management : POM, Version compatibility handled automatically
Live reload with DevTools
Auto-restart on code changes
Built-in testing support with @SpringBootTest
Error pages with useful diagnostics
Easy service discovery with Spring Cloud
Circuit breakers via Resilience4j/Netflix Hystrix
Config server for centralized configuration

Flyway vs Liquibase: Database Migration Tools

What Do Actuators Do?

Health Check - Is the app healthy? (Like a fuel gauge) -> /actuator/health → {"status":"UP"}
Metrics - Performance stats (Like a speedometer) -> /actuator/metrics → Memory usage, CPU, request counts
Environment Details - Current configurations (Like engine diagnostics) -> /actuator/env → Shows all configuration properties
Log Management - Change log levels on the fly (Like adjusting brightness) -> POST /actuator/loggers/com.example → Change logging level
Thread Dump - See all running threads (Like checking engine parts) -> /actuator/threaddump → List of active threads


What Spring Data JPA Offers Over Standard JPA
Massive Reduction in Boilerplate Code
public interface UserRepository extends JpaRepository<User, Long> {
    // All CRUD methods come for free!
}
Automatic Query Generation : List<User> findByLastNameAndAgeLessThan(String lastName, int maxAge); Generates: WHERE last_name = ?1 AND age < ?2
Pagination & Sorting : Page<User> findByLastName(String lastName, Pageable pageable); 
Methods are transactional by default, No need for @Transactional annotations on repository methods

JPA Methods :
<S extends T> S save(S entity);           // Save single entity
<S extends T> List<S> saveAll(Iterable<S> entities); // Save multiple
Optional<T> findById(ID id);             // Find by primary key
boolean existsById(ID id);               // Check if exists
List<T> findAll();                       // Get all entities
List<T> findAllById(Iterable<ID> ids);   // Get multiple by IDs
long count();                            // Get total count
<S extends T> S save(S entity);          // Updates if entity existsvoid deleteById(ID id);                  // Delete by ID
void delete(T entity);                   // Delete single entity
void deleteAll();                        // Delete all entities
void deleteAll(Iterable<? extends T> entities); // Delete multiple	

Query Derivation (From Method Names)
// Basic field queries
List<User> findByLastName(String lastName);
List<User> findByFirstNameIgnoreCase(String firstName);
List<User> findByAgeGreaterThan(int age);

// Combined conditions
List<User> findByLastNameAndFirstName(String lastName, String firstName);
List<User> findByAgeBetween(int startAge, int endAge);

// Null checks
List<User> findByMiddleNameIsNull();
List<User> findByMiddleNameIsNotNull();

// Sorting
List<User> findByLastNameOrderByFirstNameAsc(String lastName);

Custom JPQL Queries
@Query("SELECT u FROM User u WHERE u.active = true AND u.age > :minAge")
List<User> findActiveUsersByMinimumAge(@Param("minAge") int age);

@Query("UPDATE User u SET u.status = 'INACTIVE' WHERE u.lastLogin < :date")
@Modifying
void deactivateUsersNotLoggedInSince(@Param("date") LocalDate date);

Native SQL Queries
@Query(value = "SELECT * FROM users WHERE REGEXP_LIKE(email, :pattern)", 
       nativeQuery = true)
List<User> findByEmailPattern(@Param("pattern") String regexPattern);

Pagination & Sorting
Page<User> findByLastName(String lastName, Pageable pageable);
Slice<User> findTop10ByOrderBySignupDateDesc();

Asynchronous Queries
@Async
Future<User> findByUsername(String username);

@Async
CompletableFuture<List<User>> findAllByActiveTrue();

Stream Processing
@Query("SELECT u FROM User u WHERE u.status = 'ACTIVE'")
Stream<User> streamAllActiveUsers();


Is @Transactional Required in Spring Data JPA?
If you write custom implementation for repository methods @Transactional is required
All built-in CRUD methods and Query methods dont need @Transactional 

Service layer is the ideal place for @Transactional annotations

if we have long batch operations : Chunk Processing (Recommended) : Process records in smaller batches to avoid long transactions

== compares references, .equals() compares content

Comparing Content of Two Custom Objects in Java : Override equals() and hashCode() (Recommended for Most Cases)

Java Memory Model (JMM):
How threads interact through memory, When changes made by one thread become visible to others, The rules that prevent race conditions and ensure thread safety
How JMM Solves Concurrency Issues :
Using volatile
Using synchronized
Atomic Classes

In HashMap, before java8 LinkedList is used for bucket, after balanced tree are using

1. Checked Exceptions : compiler forces you to handle
FileNotFoundException
IOException
SQLException
ClassNotFoundException
2. Unchecked Exceptions : compiler doesn't force you to handle
NullPointerException
ArrayIndexOutOfBoundsException
IllegalArgumentException
ArithmeticException

Maven is build tool 
Automatically downloads libraries (JAR files) your project needs
Handles version conflicts between dependencies
Maven clean : cleans the previous build
Maven install : install and build whole application




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

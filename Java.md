
## Order of Elements in a Java Class :
```
Package Statement
Import Statements
Class Declaration

Constants (static final) # public static final int MAX_USERS = 1000;
Static variables (static) # private static int totalUsers;
Instance Variables (private first, then protected, then public)
    Primitives (boolean, byte, short, int, long, float, double)
    Immutable objects (`String`, `UUID`)
    Collections (List, Set, Map)
    Custom objects (Person, Address)

Constructors (Default, Parameterized, Static Factory, Copy Constructor, Builder Pattern)
Static Methods (Public, Private)
Instance Methods (Public, Protected, Private)
Override methods toString(), equals(), hashCode()
Private helper methods last

Inner Classes
```

## Rules of Elements in a Java Class :
```
Extends must come before implements.
Only one class can be extended, but multiple interfaces can be implemented.
Final classes cannot be extended.
Final methods cannot be overridden.
Interface methods are implicitly public abstract.
Interface variables are implicitly public static final.
Enum constants should be UPPER_CASE.
Enum methods are at bottom.
public enum Color {
    RED, GREEN, BLUE;

    public void display() {
        System.out.println("Color: " + this);
    }
}
```


## Java Collections Framework :
```
1. List (Interface) - Implementations: ArrayList, LinkedList, Vector, Stack
add(E e): Adds an element to the end of the list.
add(int index, E element): Inserts an element at the specified index.
get(int index): Retrieves an element at the specified index.
remove(int index): Removes the element at the specified index.
remove(Object o): Removes the first occurrence of the specified object.
set(int index, E element): Replaces the element at the specified index.
contains(Object o): Return true if found.
indexOf(Object o): Returns the index of the first occurrence of the specified element.
lastIndexOf(Object o): Returns the index of the last occurrence of the specified element. If not found returns -1


2. Set (Interface) - Implementations: HashSet, LinkedHashSet, TreeSet
add(E e): Adds an element to the set.
remove(Object o): Removes the specified element from the set.
contains(Object o): Checks if the set contains the specified element.
toArray(): Converts the set to an array.

3. Queue (Interface) - Implementations: PriorityQueue, LinkedList, ArrayDeque
offer(E e): Adds an element to the queue (returns false if full).
poll(): Removes and returns the front element (returns null if empty).
peek(): Retrieves the front element (returns null if empty).

4. Deque (Interface) - Implementations: ArrayDeque, LinkedList
offerFirst(E e): Adds an element at the front of the deque (returns false if full).
offerLast(E e): Adds an element at the end of the deque (returns false if full).
pollFirst(): Removes and returns the front element (returns null if empty).
pollLast(): Removes and returns the last element (returns null if empty).
peekFirst(): Retrieves the front element (returns null if empty).
peekLast(): Retrieves the last element (returns null if empty).

5. Map (Interface) - Implementations: HashMap, LinkedHashMap, TreeMap, Hashtable
put(K key, V value): Adds or updates a key-value pair in the map.
putIfAbsent(K key, V value): Adds key-value only if key is absent.
get(Object key): Retrieves the value associated with the key.
remove(Object key): Removes the key-value pair for the specified key.
containsKey(Object key): Checks if the map contains the specified key.
containsValue(Object value): Checks if the map contains the specified value.
keySet(): Returns a set of all keys in the map.
values(): Returns a collection of all values in the map.
entrySet(): Returns a set of all key-value pairs in the map.

Common methods :
size(): Returns the number of entries.
clear(): Removes all entries.
isEmpty(): Return true if no entries present.

```

## Iterators :
### List
```
for (int i = 0; i < fruits.size(); i++) System.out.println(fruits.get(i));
for (String fruit : fruits) System.out.println(fruit);
```
###  Set
```
for (String city : cities) System.out.println(city);
```
### Queue
```
while (!queue.isEmpty()) System.out.println(queue.poll());
for (String item : queue) System.out.println(item);
```
### Map
```
for (Map.Entry<Integer, String> entry : map.entrySet()) System.out.println(entry.getKey() + " : " + entry.getValue());
```

## Exceptions :

```
class CustomException extends Exception{
    public CustomException(String message) {
        super(message);
    }
}

class Main {
    
    public void getException() throws CustomException{
        throw new CustomException("Divide by zero");
    }
    
    public static void main(String[] args) {
        
        Main m = new Main();
        
        try {
            int x = 10 / 0;
        } catch (ArithmeticException e) {
            System.out.println("Exception Occured : " + e.getMessage());
        } 
        
        try {
            m.getException();
        } catch (CustomException e) {
            System.out.println("Custom Exception Occured : " + e.getMessage());
        } finally {
            System.out.println("Finally will execute anyway");
        }
        
    }
}

```

## String Methods :
```
length() - Returns the length of the string.
charAt(int index) - Returns the character at the specified index.
substring(int beginIndex) - Returns a substring from the specified start index.
substring(int beginIndex, int endIndex) - Returns a substring from the start index to the end index.
contains(CharSequence sequence) - Returns true if the string contains the specified sequence.
equals(Object anObject) - Compares the string to the specified object for equality.
equalsIgnoreCase(String anotherString) - Compares the string to the specified string, ignoring case.
compareTo(String anotherString) - Compares the string to the specified string lexicographically.
compareToIgnoreCase(String str) - Compares the string to the specified string, ignoring case, lexicographically.
startsWith(String prefix) - Returns true if the string starts with the specified prefix.
endsWith(String suffix) - Returns true if the string ends with the specified suffix.
indexOf(int ch) - Returns the index of the first occurrence of the specified character.
indexOf(String str) - Returns the index of the first occurrence of the specified substring.
lastIndexOf(int ch) - Returns the index of the last occurrence of the specified character.
lastIndexOf(String str) - Returns the index of the last occurrence of the specified substring.
replace(char oldChar, char newChar) - Returns a new string with all occurrences of oldChar replaced by newChar.
replace(CharSequence target, CharSequence replacement) - Replaces each substring of the string that matches the literal target with the specified replacement.
replaceAll(String regex, String replacement) - Replaces each substring of the string that matches the regex with the specified replacement.
replaceFirst(String regex, String replacement) - Replaces the first substring of the string that matches the regex with the specified replacement.
toLowerCase() - Converts all characters in the string to lowercase.
toUpperCase() - Converts all characters in the string to uppercase.
trim() - Removes leading and trailing whitespace from the string.
split(String regex) - Splits the string around matches of the given regular expression.
split(String regex, int limit) - Splits the string around matches of the given regular expression, with a limit on the number of splits.
concat(String str) - Concatenates the specified string to the end of the current string.
join(CharSequence delimiter, CharSequence... elements) - Joins the given elements with the specified delimiter.
valueOf(int i) - Returns the string representation of the specified integer.
toCharArray() - Converts the string into a new character array.
isEmpty() - Returns true if the string is empty (length is 0).
matches(String regex) - Returns true if the string matches the specified regular expression.
regionMatches(int toffset, String other, int ooffset, int len) - Tests if two string regions are equal.
regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len) - Tests if two string regions are equal, with an option to ignore case.
contains(CharSequence sequence) - Checks if the string contains the specified sequence of characters.
format(String format, Object... args) - Returns a formatted string using the specified format and arguments.
getBytes() - Encodes the string into a sequence of bytes using the platform's default charset.
getBytes(Charset charset) - Encodes the string into a sequence of bytes using the specified charset.
toString() - Returns the string itself (overridden from Object).
contentEquals(StringBuffer sb) - Compares the string to the specified StringBuffer for equality.
StringBuilder (mutable strings): StringBuilder sb = new StringBuilder("Hello");
String.format(): String formatted = String.format("Value: %d", 42);
StringBuffer (synchronized mutable strings): StringBuffer sb = new StringBuffer("Hello");
String Comparison: str1.equals(str2), str1.equalsIgnoreCase(str2)
```

## StringBuilder Methods :
```
StringBuilder() → Creates empty StringBuilder (capacity=16).
StringBuilder(int capacity) → Creates empty StringBuilder with given capacity.
StringBuilder(String str) → Creates StringBuilder initialized with str.
length() or capacity()
append(x) → Appends x (any type) to the end.
insert(int offset, x) → Inserts x at offset.
delete(int start, int end) → Removes chars from start to end-1.
deleteCharAt(int index) → Removes char at index.
replace(int start, int end, String str) → Replaces substring with str.
reverse() → Reverses the character sequence.
setCharAt(int index, char ch) → Sets ch at index.
substring(int start) → Returns substring from start to end.
substring(int start, int end) → Returns substring from start to end-1.
length() → Returns current length.
capacity() → Returns current capacity.
ensureCapacity(int min) → Ensures capacity ≥ min.
trimToSize() → Reduces capacity to match length.
toString() → Converts to String.
chars() → Returns IntStream of characters.
sb.setLength(0);  // Resets to "" (keeps capacity) // reuses buffer without reallocation
sb = new StringBuilder();  // Fresh empty instance // if memory optimization is needed
```

## Modifiers :

### Access Modifiers (Control Visibility)
```
public → Accessible from anywhere in the program.
protected → Accessible within the same package and subclasses.
private → Accessible only within the same class.
(default / package-private) → Accessible only within the same package (no keyword needed).
```

### Non Access Modifiers (Modify Behavior)
```
static → Belongs to the class rather than an instance.
final → Used for constants, preventing inheritance (class), and preventing method overriding.
abstract → Used in abstract classes and methods without a body.
synchronized → Used in multithreading to allow only one thread at a time.
volatile → Ensures visibility of shared variables in multithreading.
transient → Prevents a field from being serialized.
strictfp → Ensures floating-point calculations follow IEEE precision rules.
native → Used to call platform-specific (C/C++) code.
```

## Multithreading :

### Extend Thread Class

```
class Main{
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();
    }
}

public class MyThread extends Thread {
    public void run(){
        System.out.println("thread");
    }
}
```

### Implements Runnable Interface

```
class Main{
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}

public class MyRunnable implements Runnable {
    public void run(){
        System.out.println("thread");
    }
}
```

### Synchronized Method

```
public synchronized void increment() {
    count++;
}
```

### Synchronized Block

```
private final Object lock = new Object();

public void increment() {
synchronized (lock) {
    count++;
}
}
```

### Wait Notify 

```
class SharedBuffer {
    private Queue<Integer> queue = new LinkedList<>();
    private final int CAPACITY = 5;

    public synchronized void produce(int item) throws InterruptedException {
        while (queue.size() == CAPACITY) {
            wait();
        }
        queue.add(item);
        notify();
    }

    public synchronized int consume() throws InterruptedException {
        while (queue.isEmpty()) {
            wait();
        }
        int item = queue.poll();
        notify();
        return item;
    }
}
```



## Custom Sorting :

```
Arrays.sort(arr);

List<Integer> numbers = new ArrayList<>();
numbers.sort((a, b) -> b - a);

class Person {
    String name;
    int age;
}
List<Person> people = new ArrayList<>();
people.sort((p1, p2) -> p1.age - p2.age);

Set<Integer> set = new TreeSet<>((a, b) -> b - a);

PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);

List<int[]> list = new ArrayList<>();
list.sort((a, b) -> {
    if (a[0] != b[0]) {
        return a[0] - b[0];
    } else {
        return b[1] - a[1];
    }
});
```

## Enum :

### Basic Enum Syntax 

```
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

Day today = Day.MONDAY;
System.out.println(today); // Output: MONDAY

switch (today) {
    case MONDAY -> System.out.println("Week starts!");
    case FRIDAY -> System.out.println("Weekend is near!");
    default -> System.out.println("Midweek day.");
}
```

### Enum with Custom Values

```
public enum Planet {
    MERCURY(3.303e+23, 2.4397e6),
    VENUS(4.869e+24, 6.0518e6),
    EARTH(5.976e+24, 6.37814e6);

    private final double mass;   // in kilograms
    private final double radius; // in meters

    // Constructor (private by default)
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }

    // Method to calculate surface gravity
    public double surfaceGravity() {
        return 6.67300E-11 * mass / (radius * radius);
    }
}

Planet earth = Planet.EARTH;
System.out.println(earth.surfaceGravity()); // Output: 9.8 (approx)
```

### Enum with Abstract Methods

```
public enum Operation {
    ADD {
        public int apply(int a, int b) { return a + b; }
    },
    SUBTRACT {
        public int apply(int a, int b) { return a - b; }
    },
    MULTIPLY {
        public int apply(int a, int b) { return a * b; }
    };

    public abstract int apply(int a, int b); // Abstract method
}

System.out.println(Operation.ADD.apply(5, 3)); // Output: 8
System.out.println(Operation.MULTIPLY.apply(5, 3)); // Output: 15
```

### Enum Implementing Interfaces

```
public enum Task implements Runnable {
    TASK1 {
        @Override
        public void run() {
            System.out.println("Running Task 1");
        }
    },
    TASK2 {
        @Override
        public void run() {
            System.out.println("Running Task 2");
        }
    };
}
```

### Looping Through Enum Values

```
for (Day day : Day.values()) {
    System.out.println(day);
}
```

| Method            | Description                              | Example                                  |
|-------------------|------------------------------------------|------------------------------------------|
| `values()`        | Returns all enum constants               | `Day[] days = Day.values();`             |
| `valueOf(String)` | Converts a string to enum                | `Day d = Day.valueOf("MONDAY");`         |
| `name()`          | Returns the enum constant's name         | `"MONDAY".equals(Day.MONDAY.name())`     |
| `ordinal()`       | Returns the position (index) of the enum | `Day.MONDAY.ordinal()` → `0`             |


## Lambda :

### What is a Lambda Expression?

```
A lambda expression is a short block of code that: Takes parameters, Executes a block of code, Returns a result.
(parameter1, parameter2) -> { code block }

Use lambdas when:
Working with functional interfaces (Runnable, Comparator, etc.)
Using Java Streams API
Writing event listeners (e.g., button clicks)
Implementing simple single-method interfaces

Avoid when:
The logic is too complex (use a proper method instead)
You need multiple methods (use a class)
```

### Before Lambdas: The Old Way (Anonymous Classes)

```
// Old way - Anonymous class
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running!");
    }
};
runnable.run();

//With Lambda (New Way)
Runnable runnable = () -> System.out.println("Running!");
runnable.run();
```

### Lambda with Parameters

```
// Functional Interface
interface MathOperation {
    int operate(int a, int b);
}

public class Main {
    public static void main(String[] args) {
        // Lambda implementation
        MathOperation add = (a, b) -> a + b;
        System.out.println(add.operate(5, 3)); // Output: 8
    }
}
```

### Built-in Functional Interfaces

| Interface       | Method       | Example Lambda Usage             |
|-----------------|--------------|-----------------------------------|
| `Consumer<T>`   | `accept(T)`  | `(s) -> System.out.println(s)`    |
| `Supplier<T>`   | `get()`      | `() -> "Hello"`                   |
| `Function<T,R>` | `apply(T)`   | `(s) -> s.length()`              |
| `Predicate<T>`  | `test(T)`    | `(s) -> s.startsWith("A")`        |

### Method References (Shortcut for Lambdas)

| Type               | Syntax                 | Equivalent Lambda               |
|--------------------|------------------------|----------------------------------|
| Static Method      | `Math::max`            | `(a, b) -> Math.max(a, b)`       |
| Instance Method    | `System.out::println`  | `(s) -> System.out.println(s)`   |
| Constructor        | `ArrayList::new`       | `() -> new ArrayList<>()`        |

```
List<String> names = Arrays.asList("Alice", "Bob");

// Lambda
names.forEach(name -> System.out.println(name));

// Method Reference (shorter)
names.forEach(System.out::println);
```

### Real World Use Cases

**Sorting a List**
```
List<String> names = Arrays.asList("Bob", "Alice", "Charlie");

// Old way
Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});

// With Lambda
Collections.sort(names, (a, b) -> a.compareTo(b));

// Even shorter
names.sort((a, b) -> a.compareTo(b));
```

**Filtering with Streams**
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Get even numbers
List<Integer> evens = numbers.stream()
                            .filter(n -> n % 2 == 0)
                            .collect(Collectors.toList());
System.out.println(evens); // [2, 4]
```

**Thread Creation**
```
// Old way
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Thread running");
    }
}).start();

// With Lambda
new Thread(() -> System.out.println("Thread running")).start();
```

### Common Mistakes to Avoid

```
Using non-final variables in lambdas
int count = 0;
Runnable r = () -> count++; // Error: count must be final or effectively final

Overcomplicating lambdas
// Bad
Function<String, Integer> length = s -> { return s.length(); };

// Good
Function<String, Integer> length = s -> s.length();

```











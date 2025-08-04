# 🔵 Advanced Java - Collections Framework (With Detailed Examples & Method Definitions)

The Java Collections Framework provides a well-structured set of interfaces and classes to manage groups of objects. It includes data structures such as lists, sets, maps, and associated algorithms.

---

## ✅ 12. Collections Framework

### 🔹 Interfaces: List, Set, Map

* **List**: An ordered collection that allows duplicate elements.
* **Set**: A collection that does not allow duplicate elements.
* **Map**: A collection of key-value pairs, where keys are unique.

---

### 🔸 List Interface

#### ➤ ArrayList Example

```java
import java.util.*;

public class ArrayListDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Python");
        list.add("Java"); // duplicate allowed

        list.remove("Python"); // Removes "Python"
        System.out.println(list); // Output: [Java, Java]
    }
}
```

**Important Methods of ArrayList:**

* `add(E e)`: Adds element to the list
* `remove(Object o)`: Removes first occurrence of the specified element
* `get(int index)`: Returns the element at the specified position
* `set(int index, E element)`: Replaces element at the specified position
* `size()`: Returns number of elements
* `clear()`: Removes all elements

---

#### ➤ LinkedList Example

```java
import java.util.*;

public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<>();
        list.add(10);
        list.addFirst(5);
        list.addLast(20);

        System.out.println(list); // Output: [5, 10, 20]
    }
}
```

**Important Methods of LinkedList:**

* `addFirst(E e)`: Inserts at the beginning
* `addLast(E e)`: Appends at the end
* `removeFirst()`: Removes the first element
* `removeLast()`: Removes the last element
* `getFirst()`, `getLast()`: Fetches first/last elements

---

### 🔸 Set Interface

#### ➤ HashSet Example

```java
import java.util.*;

public class HashSetDemo {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Apple"); // duplicate ignored

        System.out.println(set); // Output: [Apple, Banana] (unordered)
    }
}
```

**Methods:**

* `add(E e)`: Adds element
* `remove(Object o)`: Removes specified element
* `contains(Object o)`: Returns true if element exists
* `clear()`: Clears set
* `size()`: Returns size

---

#### ➤ TreeSet Example

```java
import java.util.*;

public class TreeSetDemo {
    public static void main(String[] args) {
        Set<Integer> tree = new TreeSet<>();
        tree.add(30);
        tree.add(10);
        tree.add(20);

        System.out.println(tree); // Output: [10, 20, 30] (sorted)
    }
}
```

**TreeSet** maintains elements in **sorted order**.

---

### 🔸 Map Interface

#### ➤ HashMap Example

```java
import java.util.*;

public class HashMapDemo {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();
        map.put(1, "A");
        map.put(2, "B");
        map.put(1, "C"); // Overwrites key 1

        System.out.println(map); // Output: {1=C, 2=B}
    }
}
```

**Important Methods:**

* `put(K key, V value)`: Adds entry
* `get(Object key)`: Retrieves value
* `remove(Object key)`: Removes key-value pair
* `containsKey(Object key)`, `containsValue(Object value)`
* `keySet()`, `values()`, `entrySet()`

---

#### ➤ TreeMap Example

```java
import java.util.*;

public class TreeMapDemo {
    public static void main(String[] args) {
        TreeMap<String, Integer> map = new TreeMap<>();
        map.put("C", 3);
        map.put("A", 1);
        map.put("B", 2);

        System.out.println(map); // Output: {A=1, B=2, C=3} (sorted by key)
    }
}
```

#### ➤ LinkedHashMap Example

```java
import java.util.*;

public class LinkedHashMapDemo {
    public static void main(String[] args) {
        Map<String, String> map = new LinkedHashMap<>();
        map.put("one", "A");
        map.put("two", "B");

        System.out.println(map); // Output: {one=A, two=B} (insertion order)
    }
}
```

---

### 🔸 Iterator and ListIterator

#### ➤ Iterator

```java
import java.util.*;

public class IteratorDemo {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("A", "B", "C");
        Iterator<String> it = list.iterator();

        while(it.hasNext()) {
            System.out.print(it.next() + " ");
        }
        // Output: A B C
    }
}
```

#### ➤ ListIterator (Bidirectional)

```java
import java.util.*;

public class ListIteratorDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(List.of("X", "Y", "Z"));
        ListIterator<String> it = list.listIterator();

        while (it.hasNext()) System.out.print(it.next() + " ");
        // Output: X Y Z

        while (it.hasPrevious()) System.out.print(it.previous() + " ");
        // Output: Z Y X
    }
}
```

---

### 🔸 Comparator vs Comparable

#### ➤ Comparable (Natural Order)

```java
class Student implements Comparable<Student> {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int compareTo(Student s) {
        return this.id - s.id;
    }

    public String toString() {
        return id + "-" + name;
    }
}

public class ComparableDemo {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(3, "Ram"));
        students.add(new Student(1, "Amit"));
        students.add(new Student(2, "Zara"));

        Collections.sort(students);
        System.out.println(students); // Output: [1-Amit, 2-Zara, 3-Ram]
    }
}
```

#### ➤ Comparator (Custom Order)

```java
class Product {
    String name;
    int price;

    Product(String name, int price) {
        this.name = name;
        this.price = price;
    }

    public String toString() {
        return name + ":" + price;
    }
}

public class ComparatorDemo {
    public static void main(String[] args) {
        List<Product> products = new ArrayList<>();
        products.add(new Product("Laptop", 800));
        products.add(new Product("Mouse", 50));
        products.add(new Product("Keyboard", 70));

        products.sort((p1, p2) -> p1.price - p2.price);
        System.out.println(products); // Output: [Mouse:50, Keyboard:70, Laptop:800]
    }
}
```

---

### 🔹 Summary Table

| Interface | Implementation                  | Ordered | Duplicates | Sorted       | Thread-Safe |
| --------- | ------------------------------- | ------- | ---------- | ------------ | ----------- |
| List      | ArrayList, LinkedList           | Yes     | Yes        | No           | No          |
| Set       | HashSet, TreeSet                | No      | No         | TreeSet: Yes | No          |
| Map       | HashMap, TreeMap, LinkedHashMap | No      | Keys: No   | TreeMap: Yes | No          |

---

Use **Collections Framework** to write clean, reusable, and efficient Java code for managing data.

___


## ✅ 13. Multithreading & Concurrency

### 🔸 Thread Creation (extends Thread vs implements Runnable)

#### ➤ Using `extends Thread`

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running using Thread class");
    }

    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start(); // starts the thread
    }
}
```

#### ➤ Using `implements Runnable`

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread running using Runnable");
    }

    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}
```

### 🔸 Thread Lifecycle

States:

* **New** → **Runnable** → **Running** → **Waiting/Blocked** → **Dead**

### 🔸 synchronized, wait(), notify(), notifyAll()

```java
class Shared {
    synchronized void printTable(int n) {
        for (int i = 1; i <= 5; i++) {
            System.out.println(n * i);
        }
    }
}

class MyThread1 extends Thread {
    Shared s;
    MyThread1(Shared s) { this.s = s; }
    public void run() { s.printTable(5); }
}

class MyThread2 extends Thread {
    Shared s;
    MyThread2(Shared s) { this.s = s; }
    public void run() { s.printTable(10); }
}
```

**wait/notify Example:**

```java
class Data {
    private String packet;
    private boolean transfer = true;

    public synchronized void send(String packet) {
        while (!transfer) {
            try { wait(); } catch (InterruptedException e) {}
        }
        transfer = false;
        this.packet = packet;
        notifyAll();
    }

    public synchronized String receive() {
        while (transfer) {
            try { wait(); } catch (InterruptedException e) {}
        }
        transfer = true;
        notifyAll();
        return packet;
    }
}
```

### 🔸 ExecutorService, Callable, Future

```java
import java.util.concurrent.*;

class Task implements Callable<Integer> {
    public Integer call() throws Exception {
        return 123;
    }

    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<Integer> future = executor.submit(new Task());

        System.out.println(future.get()); // Output: 123
        executor.shutdown();
    }
}
```

### 🔸 volatile, ReentrantLock, ThreadLocal

#### ➤ volatile

```java
class VolatileDemo extends Thread {
    volatile boolean running = true;

    public void run() {
        while (running) {
            System.out.println("Running");
        }
    }

    public static void main(String[] args) throws InterruptedException {
        VolatileDemo v = new VolatileDemo();
        v.start();
        Thread.sleep(1000);
        v.running = false; // Safe visibility due to volatile
    }
}
```

#### ➤ ReentrantLock

```java
import java.util.concurrent.locks.ReentrantLock;

class LockDemo {
    public static void main(String[] args) {
        ReentrantLock lock = new ReentrantLock();
        lock.lock();
        try {
            System.out.println("Critical section");
        } finally {
            lock.unlock();
        }
    }
}
```

#### ➤ ThreadLocal

```java
public class ThreadLocalDemo {
    static ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 1);

    public static void main(String[] args) {
        Runnable task = () -> {
            threadLocal.set((int) (Math.random() * 100));
            System.out.println(Thread.currentThread().getName() + " : " + threadLocal.get());
        };

        new Thread(task).start();
        new Thread(task).start();
    }
}
```

---


## ✅ 14. File I/O and Serialization

### 🔸 Reading/Writing Files (FileReader, BufferedReader, FileWriter, BufferedWriter)

```java
import java.io.*;

public class FileIODemo {
    public static void main(String[] args) throws IOException {
        // Writing to file
        FileWriter writer = new FileWriter("example.txt");
        writer.write("Hello World");
        writer.close();

        // Reading from file
        FileReader reader = new FileReader("example.txt");
        BufferedReader br = new BufferedReader(reader);
        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
        br.close();
    }
}
```

**Key Methods:**

* `write(String)`, `close()` – FileWriter
* `readLine()`, `close()` – BufferedReader

---

### 🔸 Streams and Byte Streams (FileInputStream, FileOutputStream)

```java
import java.io.*;

public class ByteStreamDemo {
    public static void main(String[] args) throws IOException {
        String data = "Byte stream example";

        FileOutputStream fos = new FileOutputStream("data.txt");
        fos.write(data.getBytes());
        fos.close();

        FileInputStream fis = new FileInputStream("data.txt");
        int ch;
        while ((ch = fis.read()) != -1) {
            System.out.print((char) ch);
        }
        fis.close();
        // Output: Byte stream example
    }
}
```

**Key Methods:**

* `write(byte[])`, `read()`, `close()`

---

### 🔸 Serialization and `transient`

```java
import java.io.*;

class Student implements Serializable {
    int id;
    String name;
    transient int age; // won't be serialized

    Student(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }
}

public class SerializationDemo {
    public static void main(String[] args) throws Exception {
        Student s = new Student(1, "John", 25);

        // Serialize
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("student.ser"));
        oos.writeObject(s);
        oos.close();

        // Deserialize
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("student.ser"));
        Student deserialized = (Student) ois.readObject();
        ois.close();

        System.out.println(deserialized.id + " " + deserialized.name + " " + deserialized.age);
        // Output: 1 John 0 (age is transient)
    }
}
```

**Key Concepts:**

* `Serializable` interface
* `transient` keyword: prevents field from being serialized

---

### 🔸 NIO (`Path`, `Files`, `Channel`, `Buffer`)

```java
import java.nio.file.*;
import java.io.IOException;

public class NioDemo {
    public static void main(String[] args) throws IOException {
        Path path = Paths.get("nio-example.txt");

        // Write to file
        Files.write(path, "NIO File Content".getBytes());

        // Read from file
        String content = Files.readString(path);
        System.out.println(content);
        // Output: NIO File Content
    }
}
```

**NIO Classes and Methods:**

* `Paths.get(String)` – to create a Path
* `Files.readString(Path)` – read content
* `Files.write(Path, byte[])` – write content

---

## ✅ 15. Java Memory Model & JVM

### 🔸 JVM Architecture (Heap, Stack, Metaspace)

* **Heap**: Stores objects and class instances (shared).
* **Stack**: Stores method calls, local variables (per thread).
* **Metaspace**: Replaces PermGen; stores class metadata (shared).

```java
// No direct code demo, but behavior is reflected in memory usage of objects and methods.
class Sample {
    public static void main(String[] args) {
        int x = 10; // Stored in stack
        String str = new String("Hello"); // Object in heap
        System.out.println(str);
    }
}
```

---

### 🔸 ClassLoader

Responsible for loading classes into memory. Follows 3 main steps:

* **Bootstrap ClassLoader** – loads core Java classes
* **Extension ClassLoader** – loads JDK extension libraries
* **Application ClassLoader** – loads classes from classpath

```java
public class ClassLoaderDemo {
    public static void main(String[] args) {
        System.out.println(String.class.getClassLoader()); // null (bootstrap)
        System.out.println(ClassLoaderDemo.class.getClassLoader()); // Application classloader
    }
}
```

---

### 🔸 Garbage Collection (GC Types: Serial, G1, ZGC)

Garbage Collector automatically removes unused objects from memory:

* **Serial GC** – single-threaded; best for small apps
* **Parallel GC** – multi-threaded; good throughput
* **G1 GC** – low pause time, regionalized heap
* **ZGC / Shenandoah** – very low pause time, scalable

Trigger GC manually:

```java
public class GCDemo {
    public static void main(String[] args) {
        GCDemo obj = new GCDemo();
        obj = null;
        System.gc();
        // Calls finalize before GC (not guaranteed)
    }

    protected void finalize() {
        System.out.println("Object is being garbage collected");
    }
}
```

---

### 🔸 finalize() and Object Lifecycle

* `finalize()` is called by GC before object is removed.
* Not recommended anymore; replaced by **Cleaner/PhantomReference** in modern Java.

```java
class FinalizeDemo {
    protected void finalize() {
        System.out.println("finalize() called");
    }

    public static void main(String[] args) {
        FinalizeDemo f = new FinalizeDemo();
        f = null;
        System.gc();
        // Output: finalize() called (maybe)
    }
}
```

---

## ✅ 16. Inner Classes

Java allows you to define classes within classes. These are called **inner classes**, and they help logically group classes that are only used in one place.

### 🔸 Member Inner Class

```java
class Outer {
    class Inner {
        void display() {
            System.out.println("Member inner class");
        }
    }

    public static void main(String[] args) {
        Outer.Inner obj = new Outer().new Inner();
        obj.display(); // Output: Member inner class
    }
}
```

### 🔸 Static Nested Class

```java
class Outer {
    static class StaticInner {
        void display() {
            System.out.println("Static nested class");
        }
    }

    public static void main(String[] args) {
        Outer.StaticInner obj = new Outer.StaticInner();
        obj.display(); // Output: Static nested class
    }
}
```

### 🔸 Local Inner Class (inside method)

```java
class Outer {
    void outerMethod() {
        class LocalInner {
            void display() {
                System.out.println("Local inner class");
            }
        }
        LocalInner inner = new LocalInner();
        inner.display();
    }

    public static void main(String[] args) {
        new Outer().outerMethod();
        // Output: Local inner class
    }
}
```

### 🔸 Anonymous Inner Class

```java
abstract class Animal {
    abstract void sound();
}

public class AnonymousInnerDemo {
    public static void main(String[] args) {
        Animal a = new Animal() {
            void sound() {
                System.out.println("Roar");
            }
        };
        a.sound(); // Output: Roar
    }
}
```

---

### 🔸 Lambda Expressions and Functional Interfaces

A **functional interface** has exactly one abstract method. Lambdas provide a concise way to represent that method.

```java
@FunctionalInterface
interface MyFunctional {
    void show();
}

public class LambdaDemo {
    public static void main(String[] args) {
        MyFunctional f = () -> System.out.println("Lambda Expression");
        f.show(); // Output: Lambda Expression
    }
}
```

**Common Functional Interfaces (java.util.function):**

* `Consumer<T>` – takes input, returns nothing
* `Supplier<T>` – takes nothing, returns output
* `Predicate<T>` – boolean test
* `Function<T, R>` – takes input, returns output

```java
import java.util.function.*;

public class BuiltInFunctionalInterfaces {
    public static void main(String[] args) {
        Predicate<Integer> isEven = x -> x % 2 == 0;
        System.out.println(isEven.test(4)); // true

        Consumer<String> printer = s -> System.out.println(s);
        printer.accept("Hello from Consumer"); // Hello from Consumer

        Supplier<Double> random = () -> Math.random();
        System.out.println(random.get());

        Function<String, Integer> length = str -> str.length();
        System.out.println(length.apply("Java")); // 4
    }
}
```
## ✅ 17. Java 8+ Features

### 🔸 Streams API

```java
import java.util.*;
import java.util.stream.*;

public class StreamDemo {
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

        list.stream().filter(i -> i % 2 == 0).forEach(System.out::println);
        // Output: 2 4
    }
}
```

**Key Methods:**

* `stream()`, `filter()`, `map()`, `collect()`, `forEach()`

---

### 🔸 Optional Class

```java
import java.util.Optional;

public class OptionalDemo {
    public static void main(String[] args) {
        Optional<String> name = Optional.ofNullable(null);
        System.out.println(name.orElse("No Name")); // Output: No Name
    }
}
```

**Key Methods:**

* `of()`, `ofNullable()`, `isPresent()`, `orElse()`, `ifPresent()`

---

### 🔸 forEach, map, filter, reduce

```java
import java.util.*;
import java.util.stream.*;

public class StreamOps {
    public static void main(String[] args) {
        List<Integer> nums = Arrays.asList(1, 2, 3, 4);

        nums.forEach(System.out::println); // forEach

        List<Integer> doubled = nums.stream().map(n -> n * 2).collect(Collectors.toList());
        System.out.println(doubled); // [2, 4, 6, 8]

        int sum = nums.stream().reduce(0, Integer::sum);
        System.out.println(sum); // 10
    }
}
```

---

### 🔸 Date and Time API (`java.time`)

```java
import java.time.*;

public class DateTimeDemo {
    public static void main(String[] args) {
        LocalDate date = LocalDate.now();
        LocalTime time = LocalTime.now();
        LocalDateTime dateTime = LocalDateTime.now();

        System.out.println(date);
        System.out.println(time);
        System.out.println(dateTime);
    }
}
```

**Key Classes:**

* `LocalDate`, `LocalTime`, `LocalDateTime`, `Period`, `Duration`

---

### 🔸 Method References and Lambda Expressions

```java
import java.util.*;

public class MethodRefDemo {
    public static void print(String s) {
        System.out.println(s);
    }

    public static void main(String[] args) {
        List<String> list = Arrays.asList("Java", "Python", "C++");
        list.forEach(MethodRefDemo::print); // Method Reference

        list.forEach(s -> System.out.println(s)); // Lambda Expression
    }
}
```

---

### 🔸 default and static methods in interfaces

```java
interface MyInterface {
    default void show() {
        System.out.println("Default method");
    }

    static void display() {
        System.out.println("Static method in interface");
    }
}

public class InterfaceDemo implements MyInterface {
    public static void main(String[] args) {
        new InterfaceDemo().show(); // Output: Default method
        MyInterface.display(); // Output: Static method in interface
    }
}
```

---

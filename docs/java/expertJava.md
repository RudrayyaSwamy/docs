## 🔴 Expert Level
# ✅ Java Generics – Detailed Guide

Generics in Java allow you to write code that works with different data types while providing **type safety** and **code reusability**.

---

## 🔸 1. Type Parameters `<T>`

A type parameter allows a class, interface, or method to operate on objects of various types while providing compile-time type safety.

```java
// ✅ Generic Class
class Box<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}

public class TypeParameterExample {
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.setItem("Hello Generics");
        System.out.println(stringBox.getItem()); // Output: Hello Generics

        Box<Integer> intBox = new Box<>();
        intBox.setItem(42);
        System.out.println(intBox.getItem()); // Output: 42
    }
}
```

---

## 🔸 2. Wildcards `?`, `? extends`, `? super`

Wildcards allow flexibility when working with generic types.

### ✅ a. `<?>` - Unbounded Wildcard

Accepts any type, but you cannot safely add items.

```java
public static void printList(List<?> list) {
    for (Object item : list) {
        System.out.println(item);
    }
}
```

---

### ✅ b. `<? extends T>` - Upper Bounded Wildcard

Accepts T or any subclass of T (Read only, can't add new items).

```java
public static void printNumbers(List<? extends Number> numbers) {
    for (Number num : numbers) {
        System.out.println(num);
    }
}
```

```java
List<Integer> intList = Arrays.asList(1, 2, 3);
printNumbers(intList); // Output: 1 2 3
```

---

### ✅ c. `<? super T>` - Lower Bounded Wildcard

Accepts T or any superclass of T (Can add T and its subclasses).

```java
public static void addIntegers(List<? super Integer> list) {
    list.add(100);
    list.add(200);
}
```

```java
List<Number> numList = new ArrayList<>();
addIntegers(numList);
System.out.println(numList); // Output: [100, 200]
```

---

## 🔸 3. Bounded Types

Restrict the types that can be used as type arguments.

```java
class Calculator<T extends Number> {
    private T num1, num2;

    public Calculator(T num1, T num2) {
        this.num1 = num1;
        this.num2 = num2;
    }

    public double add() {
        return num1.doubleValue() + num2.doubleValue();
    }
}

public class BoundedTypeExample {
    public static void main(String[] args) {
        Calculator<Integer> calc = new Calculator<>(10, 20);
        System.out.println(calc.add()); // Output: 30.0

        Calculator<Double> dcalc = new Calculator<>(10.5, 4.5);
        System.out.println(dcalc.add()); // Output: 15.0
    }
}
```

---

## 🔸 4. Generic Methods

A method that defines its own type parameter(s).

```java
public class GenericMethods {
    // Generic method to print any array
    public static <T> void printArray(T[] array) {
        for (T item : array) {
            System.out.print(item + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Integer[] intArr = {1, 2, 3};
        String[] strArr = {"A", "B", "C"};

        printArray(intArr); // Output: 1 2 3
        printArray(strArr); // Output: A B C
    }
}
```

---

## 🔸 5. Generic Interface

```java
interface Operation<T> {
    T execute(T a, T b);
}

class AddOperation implements Operation<Integer> {
    public Integer execute(Integer a, Integer b) {
        return a + b;
    }
}

public class GenericInterfaceDemo {
    public static void main(String[] args) {
        Operation<Integer> op = new AddOperation();
        System.out.println(op.execute(5, 3)); // Output: 8
    }
}
```

---

## 🔸 6. Multiple Type Parameters

You can define multiple type parameters.

```java
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() { return key; }
    public V getValue() { return value; }
}

public class MultiTypeParam {
    public static void main(String[] args) {
        Pair<String, Integer> pair = new Pair<>("Age", 25);
        System.out.println(pair.getKey() + ": " + pair.getValue()); // Output: Age: 25
    }
}
```

---

## 🔸 7. Raw Types (Not Recommended)

Using a generic class without specifying type is called raw type.

```java
Box rawBox = new Box();  // Warning: unchecked
rawBox.setItem("Unsafe");
String s = (String) rawBox.getItem();
System.out.println(s); // Output: Unsafe
```

⚠️ **Use of raw types is discouraged** because it bypasses type checks.

---

## ✅ Summary

| Concept        | Keyword / Syntax             | Usage Example                      |
| -------------- | ---------------------------- | ---------------------------------- |
| Type Parameter | `<T>`                        | `class Box<T> { ... }`             |
| Generic Method | `<T> returnType method(T t)` | `public <T> void print(T t)`       |
| Wildcard       | `?`                          | `List<?>`, `List<? extends T>`     |
| Bounded Type   | `<T extends Number>`         | Only accept subclasses of `Number` |
| Lower Bound    | `<? super T>`                | Accept `T` or its superclasses     |

---
# ✅ Java Generics – Detailed Guide

Generics in Java allow you to write code that works with different data types while providing **type safety** and **code reusability**.

---

## 🔸 1. Type Parameters `<T>`

A type parameter allows a class, interface, or method to operate on objects of various types while providing compile-time type safety.

```java
// ✅ Generic Class
class Box<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}

public class TypeParameterExample {
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.setItem("Hello Generics");
        System.out.println(stringBox.getItem()); // Output: Hello Generics

        Box<Integer> intBox = new Box<>();
        intBox.setItem(42);
        System.out.println(intBox.getItem()); // Output: 42
    }
}
```

---

## 🔸 2. Wildcards `?`, `? extends`, `? super`

Wildcards allow flexibility when working with generic types.

### ✅ a. `<?>` - Unbounded Wildcard

Accepts any type, but you cannot safely add items.

```java
public static void printList(List<?> list) {
    for (Object item : list) {
        System.out.println(item);
    }
}
```

---

### ✅ b. `<? extends T>` - Upper Bounded Wildcard

Accepts T or any subclass of T (Read only, can't add new items).

```java
public static void printNumbers(List<? extends Number> numbers) {
    for (Number num : numbers) {
        System.out.println(num);
    }
}
```

```java
List<Integer> intList = Arrays.asList(1, 2, 3);
printNumbers(intList); // Output: 1 2 3
```

---

### ✅ c. `<? super T>` - Lower Bounded Wildcard

Accepts T or any superclass of T (Can add T and its subclasses).

```java
public static void addIntegers(List<? super Integer> list) {
    list.add(100);
    list.add(200);
}
```

```java
List<Number> numList = new ArrayList<>();
addIntegers(numList);
System.out.println(numList); // Output: [100, 200]
```

---

## 🔸 3. Bounded Types

Restrict the types that can be used as type arguments.

```java
class Calculator<T extends Number> {
    private T num1, num2;

    public Calculator(T num1, T num2) {
        this.num1 = num1;
        this.num2 = num2;
    }

    public double add() {
        return num1.doubleValue() + num2.doubleValue();
    }
}

public class BoundedTypeExample {
    public static void main(String[] args) {
        Calculator<Integer> calc = new Calculator<>(10, 20);
        System.out.println(calc.add()); // Output: 30.0

        Calculator<Double> dcalc = new Calculator<>(10.5, 4.5);
        System.out.println(dcalc.add()); // Output: 15.0
    }
}
```

---

## 🔸 4. Generic Methods

A method that defines its own type parameter(s).

```java
public class GenericMethods {
    // Generic method to print any array
    public static <T> void printArray(T[] array) {
        for (T item : array) {
            System.out.print(item + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Integer[] intArr = {1, 2, 3};
        String[] strArr = {"A", "B", "C"};

        printArray(intArr); // Output: 1 2 3
        printArray(strArr); // Output: A B C
    }
}
```

---

## 🔸 5. Generic Interface

```java
interface Operation<T> {
    T execute(T a, T b);
}

class AddOperation implements Operation<Integer> {
    public Integer execute(Integer a, Integer b) {
        return a + b;
    }
}

public class GenericInterfaceDemo {
    public static void main(String[] args) {
        Operation<Integer> op = new AddOperation();
        System.out.println(op.execute(5, 3)); // Output: 8
    }
}
```

---

## 🔸 6. Multiple Type Parameters

You can define multiple type parameters.

```java
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() { return key; }
    public V getValue() { return value; }
}

public class MultiTypeParam {
    public static void main(String[] args) {
        Pair<String, Integer> pair = new Pair<>("Age", 25);
        System.out.println(pair.getKey() + ": " + pair.getValue()); // Output: Age: 25
    }
}
```

---

## 🔸 7. Raw Types (Not Recommended)

Using a generic class without specifying type is called raw type.

```java
Box rawBox = new Box();  // Warning: unchecked
rawBox.setItem("Unsafe");
String s = (String) rawBox.getItem();
System.out.println(s); // Output: Unsafe
```

⚠️ **Use of raw types is discouraged** because it bypasses type checks.

---

## ✅ Summary

| Concept        | Keyword / Syntax             | Usage Example                      |
| -------------- | ---------------------------- | ---------------------------------- |
| Type Parameter | `<T>`                        | `class Box<T> { ... }`             |
| Generic Method | `<T> returnType method(T t)` | `public <T> void print(T t)`       |
| Wildcard       | `?`                          | `List<?>`, `List<? extends T>`     |
| Bounded Type   | `<T extends Number>`         | Only accept subclasses of `Number` |
| Lower Bound    | `<? super T>`                | Accept `T` or its superclasses     |

---

# ✅ Java Annotations and Reflection – Detailed Guide

---

## 🔸 1. Built-in Annotations

### ✅ `@Override`

Indicates that a method is overridden from a superclass.

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}

public class OverrideExample {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.sound(); // Output: Bark
    }
}
```

### ✅ `@Deprecated`

Marks a method or class as deprecated.

```java
class LegacyCode {
    @Deprecated
    void oldMethod() {
        System.out.println("This method is deprecated");
    }
}

public class DeprecatedExample {
    public static void main(String[] args) {
        new LegacyCode().oldMethod(); // Output: This method is deprecated
    }
}
```

---

## 🔸 2. Custom Annotations

### ✅ Defining an annotation

```java
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@interface Info {
    String author();
    int version();
}
```

### ✅ Using the annotation

```java
class Book {
    @Info(author = "Darshan", version = 1)
    public void display() {
        System.out.println("Book display");
    }
}
```

---

## 🔸 3. Reflection API

Used to inspect classes, methods, fields at runtime.

```java
import java.lang.reflect.*;

class Student {
    public int id;
    private String name = "John";

    public void greet() {
        System.out.println("Hello");
    }
}

public class ReflectionExample {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("Student");

        // Class name
        System.out.println("Class Name: " + clazz.getName());

        // Fields
        Field[] fields = clazz.getDeclaredFields();
        for (Field f : fields) {
            System.out.println("Field: " + f.getName());
        }

        // Methods
        Method[] methods = clazz.getDeclaredMethods();
        for (Method m : methods) {
            System.out.println("Method: " + m.getName());
        }

        // Access private field
        Object obj = clazz.getDeclaredConstructor().newInstance();
        Field privateField = clazz.getDeclaredField("name");
        privateField.setAccessible(true);
        System.out.println("Private field value: " + privateField.get(obj));
    }
}
```

### ✅ Output:

```
Class Name: Student
Field: id
Field: name
Method: greet
Private field value: John
```

---

## ✅ Summary

| Concept           | Description                                  |
| ----------------- | -------------------------------------------- |
| `@Override`       | Indicates method overrides superclass method |
| `@Deprecated`     | Marks method as deprecated                   |
| Custom Annotation | User-defined annotations                     |
| `Class`, `Method` | Part of reflection API                       |
| `Field`           | Access object fields dynamically             |

---
# ✅ Java Generics – Detailed Guide

Generics in Java allow you to write code that works with different data types while providing **type safety** and **code reusability**.

---

...\[Previous content preserved]...

---

## ✅ Summary

| Concept           | Description                                  |
| ----------------- | -------------------------------------------- |
| `@Override`       | Indicates method overrides superclass method |
| `@Deprecated`     | Marks method as deprecated                   |
| Custom Annotation | User-defined annotations                     |
| `Class`, `Method` | Part of reflection API                       |
| `Field`           | Access object fields dynamically             |

---

# ✅ Java Modules (JPMS) – Detailed Guide

The **Java Platform Module System (JPMS)** introduced in Java 9 allows modularization of code for better scalability, maintainability, and encapsulation.

---

## 🔸 1. `module-info.java`

Every module contains a `module-info.java` file that defines dependencies and exports.

### ✅ Example

```java
// module-info.java
module com.example.app {
    requires com.example.utils;
    exports com.example.app.api;
}
```

* `requires` — declares dependencies on other modules.
* `exports` — makes specific packages accessible to other modules.

---

## 🔸 2. `requires`, `exports`, `opens`

### ✅ `requires`

Declares that this module depends on another.

```java
module my.module {
    requires java.sql;
}
```

### ✅ `exports`

Makes a package visible to other modules.

```java
module my.module {
    exports com.my.package;
}
```

### ✅ `opens`

Used for deep reflection (e.g., by frameworks like Spring).

```java
module my.module {
    opens com.my.secret to some.framework;
}
```

---

## 🔸 3. Automatic and Unnamed Modules

### ✅ Automatic Modules

JARs placed on the module path **without `module-info.java`** are treated as automatic modules.

```bash
# Automatic module: name inferred from jar
lib/log4j-api-2.14.1.jar → module name: log4j.api
```

### ✅ Unnamed Module

JARs on the **classpath** are treated as part of the unnamed module and can access any exported package.

```java
// Any code in classpath (unnamed module)
// can access public types in exported modules
```

---

## 🔸 Complete Example

### ✅ Folder Structure

```
project-root/
├── app/
│   ├── module-info.java
│   └── com/example/app/MainApp.java
├── util/
│   ├── module-info.java
│   └── com/example/util/Helper.java
```

### ✅ util/module-info.java

```java
module com.example.util {
    exports com.example.util;
}
```

### ✅ app/module-info.java

```java
module com.example.app {
    requires com.example.util;
}
```

### ✅ Main Class

```java
package com.example.app;

import com.example.util.Helper;

public class MainApp {
    public static void main(String[] args) {
        Helper.greet(); // Output: Hello from util module!
    }
}
```

### ✅ Helper Class

```java
package com.example.util;

public class Helper {
    public static void greet() {
        System.out.println("Hello from util module!");
    }
}
```

---

## ✅ Summary

| Concept            | Description                                     |
| ------------------ | ----------------------------------------------- |
| `module-info.java` | Describes the module's dependencies and exports |
| `requires`         | Specifies dependent modules                     |
| `exports`          | Makes packages visible to other modules         |
| `opens`            | Allows runtime reflection access                |
| Automatic Module   | JARs on module path without `module-info.java`  |
| Unnamed Module     | Traditional classpath-based code                |

---
# ✅ Java Generics – Detailed Guide

Generics in Java allow you to write code that works with different data types while providing **type safety** and **code reusability**.

---

...\[Previous content preserved]...

---

## ✅ Summary

| Concept           | Description                                  |
| ----------------- | -------------------------------------------- |
| `@Override`       | Indicates method overrides superclass method |
| `@Deprecated`     | Marks method as deprecated                   |
| Custom Annotation | User-defined annotations                     |
| `Class`, `Method` | Part of reflection API                       |
| `Field`           | Access object fields dynamically             |

---

# ✅ Design Patterns in Java – Detailed Guide

Design patterns provide reusable solutions to common software design problems. Below are key structural, creational, and behavioral patterns.

---

## 🔸 1. Singleton Pattern

Ensures a class has only one instance and provides a global point of access.

```java
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

public class SingletonDemo {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.println(s1 == s2); // Output: true
    }
}
```

---

## 🔸 2. Factory Pattern

Creates objects without exposing the instantiation logic.

```java
interface Shape {
    void draw();
}

class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

class Square implements Shape {
    public void draw() {
        System.out.println("Drawing Square");
    }
}

class ShapeFactory {
    public Shape getShape(String type) {
        if (type.equalsIgnoreCase("circle")) return new Circle();
        if (type.equalsIgnoreCase("square")) return new Square();
        return null;
    }
}

public class FactoryDemo {
    public static void main(String[] args) {
        ShapeFactory factory = new ShapeFactory();
        Shape shape = factory.getShape("circle");
        shape.draw(); // Output: Drawing Circle
    }
}
```

---

## 🔸 3. Builder Pattern

Used to construct complex objects step by step.

```java
class Computer {
    private String CPU, RAM, storage;

    public static class Builder {
        private String CPU, RAM, storage;

        public Builder setCPU(String CPU) {
            this.CPU = CPU; return this;
        }

        public Builder setRAM(String RAM) {
            this.RAM = RAM; return this;
        }

        public Builder setStorage(String storage) {
            this.storage = storage; return this;
        }

        public Computer build() {
            Computer c = new Computer();
            c.CPU = this.CPU;
            c.RAM = this.RAM;
            c.storage = this.storage;
            return c;
        }
    }

    public void specs() {
        System.out.println("CPU: " + CPU + ", RAM: " + RAM + ", Storage: " + storage);
    }
}

public class BuilderDemo {
    public static void main(String[] args) {
        Computer comp = new Computer.Builder()
            .setCPU("i7").setRAM("16GB").setStorage("512GB SSD").build();
        comp.specs(); // Output: CPU: i7, RAM: 16GB, Storage: 512GB SSD
    }
}
```

---

## 🔸 4. Observer Pattern

Defines a one-to-many dependency between objects.

```java
import java.util.*;

interface Observer {
    void update(String message);
}

class Subscriber implements Observer {
    private String name;
    public Subscriber(String name) { this.name = name; }
    public void update(String message) {
        System.out.println(name + " received: " + message);
    }
}

class Publisher {
    private List<Observer> observers = new ArrayList<>();

    public void subscribe(Observer o) { observers.add(o); }
    public void notifyAllObservers(String message) {
        for (Observer o : observers) o.update(message);
    }
}

public class ObserverDemo {
    public static void main(String[] args) {
        Publisher pub = new Publisher();
        pub.subscribe(new Subscriber("A"));
        pub.subscribe(new Subscriber("B"));
        pub.notifyAllObservers("New Post Available!");
        // Output: A received: New Post Available!
        //         B received: New Post Available!
    }
}
```

---

## 🔸 5. Strategy Pattern

Encapsulates a family of algorithms.

```java
interface PaymentStrategy {
    void pay(int amount);
}

class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Credit Card");
    }
}

class PayPalPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}

class ShoppingCart {
    private PaymentStrategy strategy;

    public void setPaymentStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void checkout(int amount) {
        strategy.pay(amount);
    }
}

public class StrategyDemo {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        cart.setPaymentStrategy(new CreditCardPayment());
        cart.checkout(500); // Output: Paid 500 using Credit Card
    }
}
```

---

## 🔸 6. Decorator Pattern

Adds new behavior to objects dynamically.

```java
interface Coffee {
    String getDescription();
    int cost();
}

class SimpleCoffee implements Coffee {
    public String getDescription() { return "Simple Coffee"; }
    public int cost() { return 5; }
}

abstract class CoffeeDecorator implements Coffee {
    protected Coffee decorated;
    public CoffeeDecorator(Coffee c) { this.decorated = c; }
}

class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee c) { super(c); }
    public String getDescription() { return decorated.getDescription() + ", Milk"; }
    public int cost() { return decorated.cost() + 2; }
}

public class DecoratorDemo {
    public static void main(String[] args) {
        Coffee coffee = new MilkDecorator(new SimpleCoffee());
        System.out.println(coffee.getDescription()); // Output: Simple Coffee, Milk
        System.out.println(coffee.cost());           // Output: 7
    }
}
```

---

## 🔸 7. Adapter Pattern

Converts interface of a class into another interface expected by the client.

```java
interface MediaPlayer {
    void play(String fileName);
}

class VLCPlayer {
    public void playVLC(String file) {
        System.out.println("Playing VLC: " + file);
    }
}

class MediaAdapter implements MediaPlayer {
    VLCPlayer vlcPlayer = new VLCPlayer();
    public void play(String fileName) {
        vlcPlayer.playVLC(fileName);
    }
}

public class AdapterDemo {
    public static void main(String[] args) {
        MediaPlayer player = new MediaAdapter();
        player.play("movie.vlc"); // Output: Playing VLC: movie.vlc
    }
}
```

---

## 🔸 8. Proxy Pattern

Provides a surrogate or placeholder for another object.

```java
interface Image {
    void display();
}

class RealImage implements Image {
    private String filename;
    public RealImage(String filename) {
        this.filename = filename;
        loadFromDisk();
    }
    private void loadFromDisk() {
        System.out.println("Loading " + filename);
    }
    public void display() {
        System.out.println("Displaying " + filename);
    }
}

class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    public void display() {
        if (realImage == null) realImage = new RealImage(filename);
        realImage.display();
    }
}

public class ProxyDemo {
    public static void main(String[] args) {
        Image img = new ProxyImage("photo.jpg");
        img.display(); // Output: Loading photo.jpg \n Displaying photo.jpg
        img.display(); // Output: Displaying photo.jpg
    }
}
```

---

## 🔸 9. Template Method Pattern

Defines the program skeleton and allows subclasses to override specific steps.

```java
abstract class Game {
    abstract void initialize();
    abstract void startPlay();
    abstract void endPlay();

    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
}

class Football extends Game {
    void initialize() { System.out.println("Football Game Initialized"); }
    void startPlay() { System.out.println("Football Game Started"); }
    void endPlay()   { System.out.println("Football Game Finished"); }
}

public class TemplateDemo {
    public static void main(String[] args) {
        Game game = new Football();
        game.play();
        // Output:
        // Football Game Initialized
        // Football Game Started
        // Football Game Finished
    }
}
```

---

## ✅ Summary

| Pattern   | Purpose                                       |
| --------- | --------------------------------------------- |
| Singleton | One instance globally accessible              |
| Factory   | Creates object without exposing instantiation |
| Builder   | Constructs complex objects step by step       |
| Observer  | One-to-many dependency notification           |
| Strategy  | Encapsulates interchangeable behaviors        |
| Decorator | Adds behavior to object dynamically           |
| Adapter   | Converts one interface to another             |
| Proxy     | Controls access to the original object        |
| Template  | Defines algorithm skeleton in superclass      |

---

---

# ✅ Advanced Stream Operations – Detailed Guide

Java Streams offer powerful ways to work with collections of data. Below are advanced operations like parallelism, grouping, and flattening nested structures.

---

## 🔸 1. Parallel Streams

Parallel streams divide tasks across multiple threads to increase performance for large data sets.

```java
import java.util.*;
import java.util.stream.*;

public class ParallelStreamDemo {
    public static void main(String[] args) {
        List<Integer> list = IntStream.rangeClosed(1, 10).boxed().collect(Collectors.toList());

        list.parallelStream()
            .forEach(n -> System.out.println(Thread.currentThread().getName() + " -> " + n));
        // Output: Order may vary, processed by different threads
    }
}
```

---

## 🔸 2. Collectors and Grouping

Collectors help in transforming streams into lists, sets, maps, or performing grouping operations.

### ✅ Grouping by property

```java
import java.util.*;
import java.util.stream.*;

class Person {
    String name;
    String city;
    public Person(String name, String city) {
        this.name = name;
        this.city = city;
    }
    public String getCity() { return city; }
    public String getName() { return name; }
}

public class GroupingDemo {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
            new Person("Alice", "Delhi"),
            new Person("Bob", "Mumbai"),
            new Person("Charlie", "Delhi")
        );

        Map<String, List<Person>> grouped = people.stream()
            .collect(Collectors.groupingBy(Person::getCity));

        grouped.forEach((city, group) -> {
            System.out.println(city + ":");
            group.forEach(p -> System.out.println(" - " + p.getName()));
        });
        // Output:
        // Delhi:
        //  - Alice
        //  - Charlie
        // Mumbai:
        //  - Bob
    }
}
```

---

## 🔸 3. Flattening Structures (`flatMap`)

`flatMap` is used to flatten nested collections.

```java
import java.util.*;
import java.util.stream.*;

public class FlatMapDemo {
    public static void main(String[] args) {
        List<List<String>> nested = Arrays.asList(
            Arrays.asList("A", "B"),
            Arrays.asList("C", "D"),
            Arrays.asList("E")
        );

        List<String> flat = nested.stream()
            .flatMap(Collection::stream)
            .collect(Collectors.toList());

        System.out.println(flat); // Output: [A, B, C, D, E]
    }
}
```

### ✅ FlatMap with String Split

```java
List<String> lines = Arrays.asList("Java Stream", "Flat Map", "Grouping Example");

List<String> words = lines.stream()
    .flatMap(line -> Arrays.stream(line.split(" ")))
    .collect(Collectors.toList());

System.out.println(words); // Output: [Java, Stream, Flat, Map, Grouping, Example]
```

---

## ✅ Summary

| Concept         | Description                                     |
| --------------- | ----------------------------------------------- |
| Parallel Stream | Processes elements concurrently                 |
| Collectors      | Terminal ops to collect data into other forms   |
| Grouping        | Group elements based on a key                   |
| `flatMap`       | Flattens nested structures into a single stream |

---
...\[Previous content preserved]...


---

## 🔸 1. Just-In-Time (JIT) Compiler

JIT compiles bytecode into native machine code **at runtime**, optimizing performance.

### ✅ Example (Conceptual)

* Java source code ➝ compiled to bytecode ➝ interpreted by JVM ➝ JIT compiles hot code paths to native code.
* Improves speed after warm-up phase.

```java
public class JITExample {
    public static void main(String[] args) {
        long start = System.nanoTime();
        int sum = 0;
        for (int i = 0; i < 1_000_000; i++) {
            sum += i;
        }
        System.out.println("Sum: " + sum);
    }
}
// After several runs, JIT optimizes loop execution for better performance.
```

---

## 🔸 2. TLAB (Thread-Local Allocation Buffer) & Escape Analysis

### ✅ TLAB:

* Each thread gets a small region of heap (TLAB) to allocate objects without contention.
* Improves multithreaded performance.

### ✅ Escape Analysis:

* Analyzes if an object **escapes** a method.
* If not, JVM may **allocate it on the stack** instead of heap.

```java
class EscapeAnalysisDemo {
    public static void allocate() {
        Point p = new Point(10, 20); // May be allocated on stack due to escape analysis
        System.out.println(p);
    }
}

class Point {
    int x, y;
    Point(int x, int y) { this.x = x; this.y = y; }
    public String toString() { return "(" + x + ", " + y + ")"; }
}
```

---

## 🔸 3. Heap Dump & Thread Dump

### ✅ Heap Dump

* A snapshot of memory (heap) showing all objects.
* Used for memory leak analysis.

**How to generate:**

```bash
jmap -dump:format=b,file=heapdump.hprof <pid>
```

### ✅ Thread Dump

* Shows all thread states, useful for deadlock detection.

**How to generate:**

```bash
jstack <pid>
```

---

## 🔸 4. Profiling Tools

### ✅ VisualVM

* Monitors CPU, memory, threads, GC.
* Load heap dumps and perform profiling.

### ✅ JFR (Java Flight Recorder)

* Built-in low-overhead profiler.
* Use with JDK Mission Control.

**Enable with:**

```bash
java -XX:StartFlightRecording=duration=60s,filename=recording.jfr -jar MyApp.jar
```

### ✅ JConsole

* Monitors JVM performance (memory, threads, classes).

```bash
jconsole
```

---

## ✅ Summary

| Concept                 | Description                                               |
| ----------------------- | --------------------------------------------------------- |
| JIT Compiler            | Compiles bytecode to native machine code at runtime       |
| TLAB                    | Thread-local memory allocation for faster object creation |
| Escape Analysis         | JVM optimization to stack-allocate short-lived objects    |
| Heap Dump               | Snapshot of heap memory                                   |
| Thread Dump             | Snapshot of thread states                                 |
| VisualVM, JFR, JConsole | Profiling and monitoring tools                            |

---

## 🔸 1. Encryption (JCE, JCA)

Java provides two main APIs:

* **JCE (Java Cryptography Extension)** – for encryption, key generation, ciphers.
* **JCA (Java Cryptography Architecture)** – a wider API including signing, digest, encryption.

### ✅ Symmetric Encryption using AES

```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import java.util.Base64;

public class EncryptionDemo {
    public static void main(String[] args) throws Exception {
        KeyGenerator keyGen = KeyGenerator.getInstance("AES");
        keyGen.init(128);
        SecretKey secretKey = keyGen.generateKey();

        Cipher cipher = Cipher.getInstance("AES");

        // Encrypt
        cipher.init(Cipher.ENCRYPT_MODE, secretKey);
        byte[] encrypted = cipher.doFinal("Hello World".getBytes());
        String encText = Base64.getEncoder().encodeToString(encrypted);
        System.out.println("Encrypted: " + encText);

        // Decrypt
        cipher.init(Cipher.DECRYPT_MODE, secretKey);
        byte[] decrypted = cipher.doFinal(encrypted);
        System.out.println("Decrypted: " + new String(decrypted));
    }
}
// Output:
// Encrypted: (some base64 encoded text)
// Decrypted: Hello World
```

---

## 🔸 2. Secure Password Handling

Use hashing + salt. Do NOT store plaintext passwords.

### ✅ Using PBKDF2WithHmacSHA1

```java
import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.PBEKeySpec;
import java.security.SecureRandom;
import java.util.Base64;

public class PasswordHashing {
    public static void main(String[] args) throws Exception {
        String password = "mySecret123";
        byte[] salt = new byte[16];
        SecureRandom sr = new SecureRandom();
        sr.nextBytes(salt);

        PBEKeySpec spec = new PBEKeySpec(password.toCharArray(), salt, 65536, 128);
        SecretKeyFactory skf = SecretKeyFactory.getInstance("PBKDF2WithHmacSHA1");
        byte[] hash = skf.generateSecret(spec).getEncoded();

        System.out.println("Salt: " + Base64.getEncoder().encodeToString(salt));
        System.out.println("Hash: " + Base64.getEncoder().encodeToString(hash));
    }
}
// Output:
// Salt: random base64 value
// Hash: hashed password
```

---

## 🔸 3. Keystores and SSL

A **keystore** holds private keys and certificates.

### ✅ Creating a keystore with keytool

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keystore mykeystore.jks -storepass changeit
```

### ✅ Loading a keystore in Java

```java
import java.io.FileInputStream;
import java.security.KeyStore;

public class LoadKeystore {
    public static void main(String[] args) throws Exception {
        KeyStore ks = KeyStore.getInstance("JKS");
        FileInputStream fis = new FileInputStream("mykeystore.jks");
        ks.load(fis, "changeit".toCharArray());
        System.out.println("Keystore loaded with aliases: " + ks.aliases().hasMoreElements());
    }
}
```

### ✅ Enabling SSL in a Java application

Use `javax.net.ssl` package with custom trust managers or configure server libraries (like Tomcat, Jetty).

---

## ✅ Summary

| Concept              | Description                                    |
| -------------------- | ---------------------------------------------- |
| JCE/JCA              | Cryptographic libraries for encryption/signing |
| Symmetric Encryption | Encrypt using one secret key (e.g., AES)       |
| Password Hashing     | Securely store passwords using salt + hash     |
| Keystore             | Repository of keys and certificates            |
| SSL/TLS              | Secures communication channels                 |

---

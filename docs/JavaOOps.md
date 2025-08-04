
# 🟡 Intermediate Java Concepts – Full Detailed Notes with Examples

---
### ✅ 7. Object-Oriented Programming (OOP)

#### 🔹 Classes and Objects

**Class:**
- A class is a blueprint or template that defines the structure and behavior (fields and methods) of objects.
- It does not hold any real data itself until instantiated.

**Object:**
- An object is a real instance of a class.
- It has its own memory space and contains real values for the properties defined in the class.

---

#### 🧠 Why use Classes and Objects?
- To model real-world entities in code.
- Promote reusability and scalability by defining a structure that can be reused to create multiple objects.

---

#### 🧾 Example in Java:
```java
// Defining a class
class Car {
    String brand;
    int speed;

    void drive() {
        System.out.println("Driving...");
    }
}

// Using the class to create objects
public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();     // Creating an object of Car
        myCar.brand = "Toyota";    // Assigning values
        myCar.speed = 120;

        myCar.drive();             // Calling a method
        System.out.println("Brand: " + myCar.brand);
        System.out.println("Speed: " + myCar.speed + " km/h");
    }
}
```
___

#### 🔹 Constructors (default, parameterized)

**What is a Constructor?**
- A **constructor** is a special method used to initialize objects.
- It is called **automatically** when an object is created.
- Constructor name must match the class name.
- It **does not have a return type** (not even `void`).

---

#### 🧩 Types of Constructors

1. **Default Constructor**
   - Takes no parameters.
   - If you don’t write any constructor, Java automatically provides one.

```java
class Student {
    String name;

    // Default constructor
    Student() {
        name = "Unknown";
    }
}
public class Main {
    public static void main(String[] args) {
        Student s = new Student();      // Calls default constructor
        System.out.println(s.name);     // Output: Unknown
    }
}
```
1. **Parameterized  Constructor**
   - Accepts parameters to initialize object with specific values.

```java
class Student {
    String name;

    // Parameterized constructor
    Student(String name) {
        this.name = name;
    }
}
public class Main {
    public static void main(String[] args) {
        Student s = new Student("Alice");
        System.out.println(s.name);     // Output: Alice
    }
}
```
 #### Key Points:
- A class can have multiple constructors (overloaded constructors).
- If any constructor is defined explicitly, Java does not provide a default one automatically.
- You can use constructor overloading to initialize objects in different ways.
```java
class Student {
    String name;
    int age;

    // Overloaded constructors
    Student() {
        name = "Unknown";
        age = 0;
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```
### ✅ 7. Object-Oriented Programming (OOP)

#### 🔹 `this` Keyword

**What is `this`?**
- `this` is a **reference variable** in Java that refers to the **current object**.
- It is used inside instance methods or constructors to refer to the current object's fields or methods.

---

#### 🧩 Why use `this`?

1. **To differentiate between instance variables and parameters with the same name**

```java
class Student {
    String name;

    // Constructor with parameter same as instance variable
    Student(String name) {
        this.name = name;  // 'this.name' refers to instance variable
    }
}
```
2. **To call one constructor from another (constructor chaining)**
```java
class Student {
    String name;
    int age;

    // Constructor 1
    Student(String name) {
        this(name, 18);  // calls Constructor 2
    }

    // Constructor 2
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```
3. **To pass the current object as an argument**
```java
class Student {
    void display(Student s) {
        System.out.println("Method received object: " + s);
    }

    void callDisplay() {
        display(this);  // passing current object
    }
}
```
4. **To return the current object**
```java
class Student {
    String name;

    Student setName(String name) {
        this.name = name;
        return this;
    }

    void print() {
        System.out.println("Name: " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();
        s.setName("Rahul").print();  // method chaining
    }
}
```
 #### Key Points:
- this is only used within non-static context (inside instance methods or constructors).
- It improves readability, prevents confusion, and enables constructor chaining.
- You cannot use this in a static method since static methods belong to the class, not the object.

___

#### 🔹 Encapsulation (getters/setters)

**Definition:**  
Encapsulation is the process of **binding data (fields)** and **code (methods)** together and restricting access to some components. This is achieved using **access modifiers** like `private`, `public`, and **getter/setter** methods.

**Purpose:**  
- Protect data from unauthorized access.
- Control how data is accessed/modified.

**Example:**
```java
class Person {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```
#### 🔹 Inheritance (extends, super)
**Definition:**
Inheritance allows a class (subclass) to inherit fields and methods from another class (superclass).

##### Keywords:
**extends**: Inherits from a class.

**super**: Refers to parent class.
```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void sound() {
        super.sound();
        System.out.println("Dog barks");
    }
}
```
#### 🔹 Polymorphism (Overloading & Overriding)
**Definition:**
Polymorphism means many forms. It allows the same method name to behave differently based on context.

1. **Method Overloading (Compile-time)**
```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}
```
2. **Method Overriding (Runtime)**
```java
class Animal {
    void makeSound() {
        System.out.println("Generic sound");
    }
}

class Cat extends Animal {
    void makeSound() {
        System.out.println("Meow");
    }
}
```
#### 🔹 Abstraction (abstract class, interfaces)
**Definition:**
Abstraction means hiding internal implementation and showing only essential details.

1. **Abstract Class:**
```java
abstract class Shape {
    abstract void draw();
    void display() {
        System.out.println("Shape displayed");
    }
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing circle");
    }
}
```
2. **interface**
```java
interface Vehicle {
    void start();
}

class Bike implements Vehicle {
    public void start() {
        System.out.println("Bike started");
    }
}
```
#### 🔹 Access Modifiers: public vs private vs protected vs default
| Modifier    | Class | Package | Subclass | World |
| ----------- | ----- | ------- | -------- | ----- |
| `private`   | ✅     | ❌       | ❌        | ❌     |
| (default)   | ✅     | ✅       | ❌        | ❌     |
| `protected` | ✅     | ✅       | ✅        | ❌     |
| `public`    | ✅     | ✅       | ✅        | ✅     |
___
✅ = Accessible | ❌ = Not Accessible

**private:** Accessible only within the same class.

**default (no modifier)**: Accessible within the same package.

**protected**: Accessible in same package and in subclasses.

**public**: Accessible from anywhere.

#### 🔹 2. super vs this
| Feature      | `this`                          | `super`                                    |
| ------------ | ------------------------------- | ------------------------------------------ |
| Refers to    | Current object                  | Immediate parent class                     |
| Used in      | Instance methods & constructors | Subclass constructors & overridden methods |
| Constructor  | Calls current class constructor | Calls parent class constructor             |
| Field access | Access current class fields     | Access parent class fields                 |

```java
this.name = name;         // Refers to current class field
super.name = name;        // Refers to parent class field
```
####🔹 3. Overloading vs Overriding
| Feature              | Overloading                            | Overriding                                                 |
| -------------------- | -------------------------------------- | ---------------------------------------------------------- |
| Definition           | Same method name, different parameters | Subclass provides specific implementation of parent method |
| Compile-time/Runtime | Compile-time                           | Runtime                                                    |
| Inheritance          | Not required                           | Required                                                   |
| Access Modifier      | Can be anything                        | Cannot be more restrictive than parent                     |
| Static Methods       | Can be overloaded                      | Cannot be overridden (only hidden)                         |
___

Example Overloading:
```java
void display() {}
void display(int a) {}
```
Example Overriding:
```java
class A { void display() {} }
class B extends A { void display() {} }
```
#### 🔹 4. Abstract Class vs Interface
| Feature              | Abstract Class                     | Interface                                          |
| -------------------- | ---------------------------------- | -------------------------------------------------- |
| Type                 | Partial abstraction                | Full abstraction (Java 7)                          |
| Keywords             | `abstract class`                   | `interface`                                        |
| Constructors         | Allowed                            | Not allowed                                        |
| Variables            | Can be final, static, non-static   | `public static final` only                         |
| Methods              | Can have method body               | Cannot (Java 7), default/static allowed in Java 8+ |
| Multiple Inheritance | Not supported                      | Supported                                          |
| Use-case             | Common base class with shared code | Common contract for unrelated classes              |
___
Abstract Class Example:
```java
abstract class Shape {
    abstract void draw();
    void info() { System.out.println("Shape"); }
}
```
Interface Example:
```java
interface Drawable {
    void draw();
}
```
#### 🔹 5. Static vs Non-static
| Feature     | `static`                           | Non-static (instance)      |
| ----------- | ---------------------------------- | -------------------------- |
| Belongs to  | Class                              | Object                     |
| Accessed by | ClassName or object                | Only by object             |
| Memory      | Allocated once in class area       | Allocated with each object |
| Can access  | Only static members                | Static + instance members  |
| Used for    | Utilities, constants, shared logic | Object-specific logic      |
___
```java
class Example {
    static int count = 0;           // Shared among all instances
    int id;                         // Separate for each object

    static void printCount() {
        System.out.println(count);
    }

    void printId() {
        System.out.println(id);
    }
}
```
___
### ✅ 8. Access Modifiers

Java provides four types of access modifiers to set the visibility or accessibility of classes, methods, and variables.

---

#### 🔹 Types of Access Modifiers

| Modifier    | Class | Package | Subclass (different package) | World |
|-------------|-------|---------|------------------------------|--------|
| `private`   | ✅     | ❌       | ❌                            | ❌     |
| *default*   | ✅     | ✅       | ❌                            | ❌     |
| `protected` | ✅     | ✅       | ✅                            | ❌     |
| `public`    | ✅     | ✅       | ✅                            | ✅     |

✅ = Accessible | ❌ = Not Accessible

---

#### 🔹 1. `private`

- Accessible only within the **same class**.
- Not accessible from outside the class, even in the same package.

**Example:**
```java
class A {
    private int data = 40;

    private void msg() {
        System.out.println("Hello private");
    }
}
```
#### 🔹 2. `default` (no modifier)
- Accessible only within the same package.
- Not accessible from outside the package.
**Example:**
```java
class A {  // default class
    int data = 50;  // default field

    void msg() {    // default method
        System.out.println("Default access");
    }
}
```
####  3.`protected`
- Accessible within the same package.
- Accessible outside the package only via inheritance.
**Example:**
```java
package package1;
public class A {
    protected void msg() {
        System.out.println("Hello protected");
    }
}

package package2;
import package1.A;

class B extends A {
    public static void main(String args[]) {
        B obj = new B();
        obj.msg();  // Accessible because B extends A
    }
}
```
#### 🔹 4. `public`
- Accessible from anywhere in the program.
- No restriction on access.
**Example:**
```java
public class A {
    public int data = 100;

    public void msg() {
        System.out.println("Hello public");
    }
}
```
#### Key Notes
- Use `private` for data hiding (encapsulation).
- Use `public` for APIs or global access.
- Use `protected` for access in child classes across packages.
- `default` is package-private and should be used for package-level scope.

### ✅ 9. String Handling

String handling is a crucial part of Java. Java provides various classes like `String`, `StringBuilder`, and `StringBuffer` to work with strings efficiently.

---

#### 🔹 String Class and Common Methods

**String** in Java is an object that represents a sequence of characters. It is immutable, meaning once created, its value cannot be changed.

**Common Methods:**
```java
String s = "Hello, World!";

s.length();              // Returns length of string
s.charAt(0);             // Returns character at index 0 => 'H'
s.substring(0, 5);       // Returns "Hello"
s.toUpperCase();         // Converts to "HELLO, WORLD!"
s.toLowerCase();         // Converts to "hello, world!"
s.replace("World", "Java"); // "Hello, Java!"
s.contains("Hello");     // true
s.equals("hello");       // false (case-sensitive)
s.equalsIgnoreCase("hello, world!"); // true
```
***Example:**
```java
public class StringExample {
    public static void main(String[] args) {
        String name = "Java";
        System.out.println(name.toUpperCase()); // JAVA
        System.out.println(name.substring(1));  // ava
    }
}
```
#### 🔹 StringBuilder vs StringBuffer
Both are mutable classes used to manipulate strings, but they differ in synchronization.
___
| Feature       | `StringBuilder`          | `StringBuffer`                  |
| ------------- | ------------------------ | ------------------------------- |
| Mutability    | Mutable                  | Mutable                         |
| Thread-safe   | ❌ Not thread-safe        | ✅ Thread-safe                   |
| Performance   | Faster (single-threaded) | Slower (due to synchronization) |
| Introduced in | Java 5                   | Java 1.0                        |

___
**Example (StringBuilder):**
```java
public class BuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World");
        System.out.println(sb);  // Hello World
    }
}
```
**Example (StringBuffer):**
```java
public class BufferExample {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Hello");
        sb.append(" Java");
        System.out.println(sb);  // Hello Java
    }
}
```
#### 🔹 Immutability 
- String objects are `immutable` — you cannot change the value after creation.
- Any modification results in a new object being created.
- Use s = s.concat(" World"); to modify.

```java
String s = "Hello";
s.concat(" World"); 
System.out.println(s); // Output: Hello (unchanged)
```
---
#### 🔹  Interning:
- Java uses a String pool to store string literals.
- When you create a string literal, Java checks if it already exists in the pool.
- Use intern() to get pooled reference:

**Example :**
```java
String a = "Java";
String b = "Java";
System.out.println(a == b);  // true (same reference)

String c = new String("Java");
System.out.println(a == c);  // false (different object)

// Use intern() to get pooled reference:
System.out.println(a == c.intern()); // true
```
#### 📝 Summary Notes:
- String is immutable; use StringBuilder or StringBuffer for mutable strings.
- Use StringBuilder for better performance when not working with threads.
- StringBuffer is safer for multi-threaded environments.
- Interning helps Java optimize memory for repeated string literals.

✅ StringExample.java
```java
public class StringExample {
    public static void main(String[] args) {
        String s = "  Hello World  ";

        System.out.println("Original: '" + s + "'");                  // '  Hello World  '
        System.out.println("Trimmed: '" + s.trim() + "'");           // 'Hello World'
        System.out.println("Length: " + s.length());                 // 15
        System.out.println("Uppercase: " + s.toUpperCase());         // '  HELLO WORLD  '
        System.out.println("Lowercase: " + s.toLowerCase());         // '  hello world  '
        System.out.println("Char at 1: " + s.charAt(1));             // ' '
        System.out.println("Substring(2, 7): " + s.substring(2, 7)); // 'Hello'
        System.out.println("Replace 'World' with 'Java': " + s.replace("World", "Java")); // '  Hello Java  '
        System.out.println("Contains 'Hello': " + s.contains("Hello")); // true
        System.out.println("Starts with 'He': " + s.startsWith("He"));   // false (starts with space)
        System.out.println("Ends with 'ld': " + s.endsWith("ld"));       // false (ends with space)
        System.out.println("Equals 'hello world': " + s.equals("hello world")); // false
        System.out.println("Equals Ignore Case: " + s.equalsIgnoreCase("  hello world  ")); // true
        System.out.println("Index of 'o': " + s.indexOf('o'));         // 6
        System.out.println("Last Index of 'l': " + s.lastIndexOf('l')); // 9

        String[] parts = s.trim().split(" "); // Splits "Hello World"
        System.out.println("Split by space:");
        for (String part : parts) {
            System.out.println(part); // Hello \n World
        }

        System.out.println("Join: " + String.join("-", "Java", "Python", "C++")); // Java-Python-C++
        System.out.println("To Char Array:");
        for (char ch : s.toCharArray()) {
            System.out.print(ch + " "); // prints characters with space
        }

        String s2 = new String("Hello");
        String s3 = "Hello";
        System.out.println("\nInterned equals: " + (s2.intern() == s3)); // true
    }
}
```
✅ StringBuilderExample.java
```java
public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Java");

        sb.append(" Programming"); // "Java Programming"
        System.out.println("Append: " + sb);

        sb.insert(5, "Language "); // "Java Language Programming"
        System.out.println("Insert: " + sb);

        sb.replace(5, 13, "Core "); // "Java Core Programming"
        System.out.println("Replace: " + sb);

        sb.delete(5, 10); // "JavaProgramming"
        System.out.println("Delete: " + sb);

        sb.setCharAt(0, 'j'); // "javaProgramming"
        System.out.println("Set Char At: " + sb);

        System.out.println("Reverse: " + sb.reverse()); // "gnimmargorPavaj"
        sb.reverse(); // restore to "javaProgramming"

        System.out.println("Length: " + sb.length()); // 16
        System.out.println("Capacity: " + sb.capacity()); // default 16 + initial string length

        sb.ensureCapacity(100); // no visible output
        System.out.println("Capacity after ensure: " + sb.capacity()); // >= 100

        System.out.println("To String: " + sb.toString()); // "javaProgramming"
    }
}
```
✅ StringBufferExample.java
```java
public class StringBufferExample {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Thread");

        sb.append(" Safe"); // "Thread Safe"
        System.out.println("Append: " + sb);

        sb.insert(7, "Java "); // "Thread Java Safe"
        System.out.println("Insert: " + sb);

        sb.replace(7, 12, "Multi-Threaded "); // "Thread Multi-Threaded Safe"
        System.out.println("Replace: " + sb);

        sb.delete(7, 22); // "Thread Safe"
        System.out.println("Delete: " + sb);

        sb.setCharAt(0, 't'); // "thread Safe"
        System.out.println("Set Char At: " + sb);

        System.out.println("Reverse: " + sb.reverse()); // "efaS daerht"
        sb.reverse(); // restore

        System.out.println("Length: " + sb.length()); // 11
        System.out.println("Capacity: " + sb.capacity()); // default 16 + initial string length

        System.out.println("To String: " + sb.toString()); // "thread Safe"
    }
}

```
---
### ✅ 10. Exception Handling in Java

Java provides a powerful exception-handling mechanism to gracefully manage runtime errors and maintain the normal flow of the application.

---

### 🔹 `try`, `catch`, `finally`, `throw`, `throws`

#### ✅ `try-catch-finally` Block

The `try` block contains code that might throw exceptions. The `catch` block handles the exception. The `finally` block is always executed regardless of exception occurrence.

```java
public class TryCatchFinallyExample {
    public static void main(String[] args) {
        try {
            int a = 5 / 0;
        } catch (ArithmeticException e) {
            System.out.println("Caught exception: " + e.getMessage());
        } finally {
            System.out.println("Finally block always executes.");
        }
    }
}
// Output:
// Caught exception: / by zero
// Finally block always executes.
```
#### ✅ `throw` Keyword
- Used to explicitly throw an exception from a method or block.
```java
public class ThrowExample {
    public static void main(String[] args) {
        int age = 16;
        if (age < 18) {
            throw new ArithmeticException("Age must be at least 18.");
        }
        System.out.println("Eligible for voting.");
    }
}
// Output: Exception in thread "main" java.lang.ArithmeticException: Age must be at least 18.
```
#### ✅ `throws` Keyword
Used in method signature to declare checked exceptions that the method might throw.
```java
public class ThrowsExample {
    static void checkFile() throws java.io.IOException {
        throw new java.io.IOException("File error occurred.");
    }

    public static void main(String[] args) {
        try {
            checkFile();
        } catch (java.io.IOException e) {
            System.out.println("Handled Exception: " + e.getMessage());
        }
    }
}
// Output: Handled Exception: File error occurred.
```
#### 🔹 Checked vs Unchecked Exceptions
| Type                | Description                                | Example Classes                           |
| ------------------- | ------------------------------------------ | ----------------------------------------- |
| Checked Exception   | Must be handled or declared using `throws` | IOException, SQLException                 |
| Unchecked Exception | Runtime exceptions, not required to handle | NullPointerException, ArithmeticException |

___
**Checked Exception**
```java
import java.io.FileReader;
import java.io.FileNotFoundException;

public class CheckedExample {
    public static void main(String[] args) {
        try {
            FileReader fr = new FileReader("file.txt");
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
```
**Unchecked Exception**
```java
public class UncheckedExample {
    public static void main(String[] args) {
        int[] arr = new int[3];
        System.out.println(arr[5]); // ArrayIndexOutOfBoundsException
    }
}
```
**Custem Exception**
- You can create your own exception class by extending Exception or RuntimeException.
```java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public class CustomExceptionDemo {
    static void validate(int age) throws InvalidAgeException {
        if (age < 18)
            throw new InvalidAgeException("Not eligible for vote");
    }

    public static void main(String[] args) {
        try {
            validate(16);
        } catch (InvalidAgeException e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
// Output: Caught: Not eligible for vote
```
#### 📝 Summary Notes
- Always handle checked exceptions using `try-catch` or `throws`.
- Unchecked exceptions are optional to handle.
- Use `finally` for cleanup (e.g., closing resources).
- Create `custom exceptions` for domain-specific validations.

___

## ✅ 11. Packages & Imports in Java

---

### 🔹 What is a Package?

A **package** is a namespace that organizes classes and interfaces. Think of it as a folder in your system where related Java files are grouped.

- Helps avoid class name conflicts
- Makes code easier to maintain

---

### 🔹 Types of Packages

| Type          | Example            |
|---------------|--------------------|
| Built-in      | `java.lang`, `java.util`, `java.io` |
| User-defined  | `com.myapp.utils`, `tech.vismo.service` |

---

### 🔹 Creating and Using User-defined Packages

**Step 1:** Create a class inside a package
📁 File: `mypack/MessagePrinter.java`
```java
package mypack;

public class MessagePrinter {
    public void print() {
        System.out.println("Hello from mypack!");
    }
}
```
**Step 2:** Use it in another class
📁 File: TestPackage.java
```java
import mypack.MessagePrinter;

public class TestPackage {
    public static void main(String[] args) {
        MessagePrinter mp = new MessagePrinter();
        mp.print(); // Output: Hello from mypack!
    }
}
```
- 🧠 Make sure to place the mypack folder correctly in your source directory.

**🔹 `import` Keyword**
- Used to access classes from other packages.
- Makes code cleaner by avoiding fully qualified names.
```java 
import java.util.Scanner; // import specific class
import java.util.*; // import entire util package
```
```java
java.util.Scanner sc = new java.util.Scanner(System.in);
// Without import, you'd have to write:
```
**🔹 `Default` Package**
If no package is defined, the class is in the default package (not recommended for real projects).
| Package     | Description                           | Example Classes                      |
| ----------- | ------------------------------------- | ------------------------------------ |
| `java.lang` | Default basic classes (auto-imported) | `String`, `Math`, `System`, `Object` |
| `java.util` | Utility classes                       | `ArrayList`, `HashMap`, `Scanner`    |
| `java.io`   | Input/Output classes                  | `File`, `BufferedReader`             |
| `java.net`  | Networking                            | `Socket`, `URL`                      |
| `java.sql`  | Database connectivity                 | `Connection`, `DriverManager`        |

#### Example with built in packages
```java
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter name: ");
        String name = sc.nextLine();
        System.out.println("Hello, " + name); // Output depends on input
        sc.close();
    }
}
```
#### 📝 Summary
- Packages help organize and reuse code.
- Use `package` to declare a package.
- Use `import`to access classes from other packages.
- `java.lang` is automatically imported.
- Always close resources like Scanner or FileReader.
### ✅ 1. Java Basics (Explained Simply)

---

#### 🔸 What is Java? (Features)

Java is a **programming language** used to build applications (websites, mobile apps, games, etc.).  
It's also a **platform** because it runs on the **Java Virtual Machine (JVM)**.

**Key Features:**
- 🧠 **Simple** – Easy to learn and use.
- 🔄 **Object-Oriented** – Uses objects and classes to organize code.
- 💻 **Platform Independent** – Runs on any device with a JVM (`Write Once, Run Anywhere`).
- 🛡️ **Secure** – Protects against viruses and memory access issues.
- ⚙️ **Robust** – Handles errors and manages memory well.
- 🔀 **Multithreaded** – Can perform multiple tasks at once.

---

#### 🔸 Installing JDK, JVM, JRE

- **JDK (Java Development Kit):** Tools needed to write and run Java programs (includes compiler, debugger, etc.).
- **JRE (Java Runtime Environment):** Allows you to run Java programs (includes JVM + libraries).
- **JVM (Java Virtual Machine):** Executes Java bytecode on your computer.

✅ To code in Java, install the **JDK** (which includes both JRE and JVM).

---

#### 🔸 Java Program Structure

A typical Java program looks like this:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}

```
- class HelloWorld → Every program is inside a class.
- main() method → Entry point; program starts here.
- System.out.println() → Prints to the console.

#### 🔸 Writing Your First Program (HelloWorld)

**Steps:**

1. Open a text editor or IDE (like VS Code or IntelliJ).
2. Write the `HelloWorld` code shown above.
3. Save the file as `HelloWorld.java`.

---

#### 🔸 Compilation and Execution Flow

✅ **Compile:**  
Run the following command:  
```bash
javac HelloWorld.java
```

➡️ Converts source code into bytecode (HelloWorld.class)

▶️ **Run:**
Run the following command:
```bash
java HelloWorld
```
➡️ JVM executes the program and prints:
```bash
Hello, world!
```
| Step              | Output              |
|-------------------|---------------------|
| Source Code       | `.java` file        |
| Compilation       | `.class` bytecode   |
| Execution (JVM)   | Program runs        |
---

### ✅ 2. Data Types and Variables (Explained Simply)

---

#### 🔸 Primitive Data Types (`int`, `float`, `char`, etc.)

These are **basic types** built into Java.  
They store **single values** and are not objects.

| Type     | Example              | Description                        |
|----------|----------------------|------------------------------------|
| `int`    | `int age = 25;`      | Stores whole numbers               |
| `float`  | `float pi = 3.14f;`  | Stores decimal numbers (use `f`)   |
| `double` | `double d = 10.56;`  | Stores large decimal numbers       |
| `char`   | `char grade = 'A';`  | Stores a single character          |
| `boolean`| `boolean isOn = true;` | Stores true or false              |
| `byte`   | `byte b = 100;`      | Very small integer (1 byte)        |
| `short`  | `short s = 20000;`   | Small integer (2 bytes)            |
| `long`   | `long l = 100000L;`  | Large integer (add `L` at the end) |

---

#### 🔸 Reference Data Types

Reference types store the **memory address** of an object.

Examples:
```java
String name = "John";
int[] numbers = {1, 2, 3};
```
They are used for objects like:


#### 🔸 Type Casting (Implicit and Explicit)

**Type Casting** means converting one data type into another.

✅ **Implicit Casting** (Widening Conversion)  
Automatically converts a **smaller type to a larger type**. No data is lost.

```java
int a = 10;
double b = a;  // int is automatically converted to double
```
✅ **Explicit Casting** (Narrowing Conversion)  
Manually converts a **larger type to a smaller type**. May lose data.
```java
double x = 10.5;
int y = (int) x; // double is cast to int, decimal part is lost
```
🔒 **`final`** – Used to create **constants**. Once assigned, the value **cannot be changed**.

✅ Example:

```java
final int MAX_USERS = 100;// MAX_USERS = 200; // ❌ Error: cannot assign a value to final variable
```

🌐 **`static`** – Belongs to the **class**, not to individual objects.  
It is **shared** among all instances of the class.

---

✅ **Example:**

```java
class Counter {
    static int count = 0;  // static variable shared by all instances

    Counter() {
        count++;           // increment count whenever an object is created
    }
}

public class Main {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        Counter c3 = new Counter();

        System.out.println(Counter.count); // Output: 3
    }
}
```
📝 Explanation:

- The count variable is marked as static, so it's not tied to a specific object.
- No matter how many objects (c1, c2, c3) are created, they share the same static variable.
- This is why Counter.count gives 3 — the total number of objects created.

---

✨ **`var`** (Java 10+) – Automatically detects the **data type** based on the assigned value.

✅ **Example:**

```java
var name = "Alice";   // treated as String
var age = 30;         // treated as int
var price = 99.99;    // treated as double
```

✅**Note**: var can only be used inside methods, not for class-level variables or fields.
❌**Invalid Usage**:
```java
class Test {
    var a = 10;  // ❌ Error: 'var' is not allowed at class level
}
```
✅**Valid Usage**:
```java
public class Main {
    public static void main(String[] args) {
        var message = "Hello Java";  // ✅ OK inside method
    }
}
```
---
### ✅ 3. Operators (Explained Simply)

Java operators are special symbols that perform operations on variables and values.

---

#### 🔸 Arithmetic Operators

Used for **basic math** operations.

| Operator | Description        | Example        | Result      |
|----------|--------------------|----------------|-------------|
| `+`      | Addition            | `5 + 3`        | `8`         |
| `-`      | Subtraction         | `5 - 3`        | `2`         |
| `*`      | Multiplication      | `5 * 3`        | `15`        |
| `/`      | Division            | `10 / 2`       | `5`         |
| `%`      | Modulus (remainder) | `10 % 3`       | `1`         |

---

#### 🔸 Relational (Comparison) Operators

Used to compare two values. Returns `true` or `false`.

| Operator | Description             | Example     | Result     |
|----------|-------------------------|-------------|------------|
| `==`     | Equal to                | `5 == 5`    | `true`     |
| `!=`     | Not equal to            | `5 != 3`    | `true`     |
| `>`      | Greater than            | `5 > 3`     | `true`     |
| `<`      | Less than               | `5 < 3`     | `false`    |
| `>=`     | Greater than or equal   | `5 >= 5`    | `true`     |
| `<=`     | Less than or equal      | `4 <= 3`    | `false`    |

---

#### 🔸 Logical Operators

Used to combine multiple boolean expressions.

| Operator | Description         | Example              | Result     |
|----------|---------------------|----------------------|------------|
| `&&`     | Logical AND         | `true && false`      | `false`    |
| `||`     | Logical OR          | `true || false`      | `true`     |
| `!`      | Logical NOT         | `!true`              | `false`    |

---

#### 🔸 Assignment and Unary Operators

**Assignment Operators:**
Used to assign values to variables.

```java
int x = 10;
x += 5;  // same as x = x + 5;
```
| Operator | Meaning             |
| -------- | ------------------- |
| `=`      | Assign              |
| `+=`     | Add and assign      |
| `-=`     | Subtract and assign |
| `*=`     | Multiply and assign |
| `/=`     | Divide and assign   |
| `%=`     | Modulus and assign  |
---
### 🔸 Unary Operators

Used with a **single operand** to perform operations like increment, decrement, or negation.

| Operator | Description   | Example   | Result    |
|----------|---------------|-----------|-----------|
| `+`      | Unary plus    | `+x`      | `+10`     |
| `-`      | Unary minus   | `-x`      | `-10`     |
| `++`     | Increment     | `x++`     | `x + 1`   |
| `--`     | Decrement     | `x--`     | `x - 1`   |
| `!`      | Logical NOT   | `!true`   | `false`   |

---

### 🔸 Ternary Operator

Used as a **shorthand for if-else** statements.

✅ Example:

```java
int age = 18;
String result = (age >= 18) ? "Adult" : "Minor";
```
✅ If the condition is true, it returns `"Adult"`, else `"Minor"`.

📌 **Syntax:**
```java
(condition) ? value_if_true : value_if_false;

```

### 🔸 Bitwise Operators

Used for operations on **bits** (binary values).

| Operator | Description         | Example     |
|----------|---------------------|-------------|
| `&`      | Bitwise AND         | `a & b`     |
| `|`      | Bitwise OR          | `a | b`     |
| `^`      | Bitwise XOR         | `a ^ b`     |
| `~`      | Bitwise Complement  | `~a`        |
| `<<`     | Left shift          | `a << 2`    |
| `>>`     | Right shift         | `a >> 2`    |

📝 **Explanation**:
- `a & b`: Bit is 1 only if **both** bits are 1.
- `a | b`: Bit is 1 if **either** bit is 1.
- `a ^ b`: Bit is 1 if bits are **different**.
- `~a`: Inverts (flips) all bits.
- `a << n`: Shifts bits **left** by `n` (multiplies by 2ⁿ).
- `a >> n`: Shifts bits **right** by `n` (divides by 2ⁿ).

---

### 🔸 Precedence and Associativity

**Operator precedence** defines the **order** in which operators are evaluated.

✅ **Higher precedence** operators are evaluated **before** lower precedence ones.

📌 **Example:**

```java
int result = 10 + 2 * 5;  // result = 10 + (2 * 5) = 20
```

### ✅ 4. Control Statements

Control statements allow the program to make decisions and repeat actions.

---

#### 🔸 `if`, `else if`, `else`

Used for decision-making based on conditions.

```java
int age = 18;

if (age < 18) {
    System.out.println("Minor");
} else if (age == 18) {
    System.out.println("Just became adult");
} else {
    System.out.println("Adult");
}
```

✅ The first matching condition is executed, others are skipped.

---

#### 🔸 `switch` Statement

Used to select one of many code blocks to be executed.

```java
int day = 2;

switch (day) {
    case 1: System.out.println("Sunday"); break;
    case 2: System.out.println("Monday"); break;
    default: System.out.println("Invalid day");
}
```

✅ `break` prevents fall-through to next cases.

---

#### 🔸 Loops (`while`, `do-while`, `for`)

Used to **repeat a block of code**.

🔹 `while` loop – checks condition **before** execution:

```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

🔹 `do-while` loop – runs the code **at least once**, checks condition **after**:

```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
```

🔹 `for` loop – most common, compact form:

```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

---

#### 🔸 `break`, `continue`, `return`

🔹 `break` – exits the current loop or switch:

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) break;
    System.out.println(i);
}
// Output: 1 2
```

🔹 `continue` – skips the current iteration:

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    System.out.println(i);
}
// Output: 1 2 4 5
```

🔹 `return` – exits from the method completely:

```java
public void greet() {
    System.out.println("Hello");
    return;
    // Code here won’t execute
}
```
### ✅ 5. Arrays

Arrays store multiple values of the same type in a single variable.

---

#### 🔸 1D Arrays

A linear collection of elements.

```java
int[] numbers = {10, 20, 30, 40};
System.out.println(numbers[0]); // Output: 10
```
You can also initialize with size:
```java
int[] arr = new int[5];  // default values = 0
arr[0] = 100;
```
#### 🔸 2D Arrays
An array of arrays (like a matrix or table):
```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

System.out.println(matrix[1][2]);  // Output: 6
```
#### 🔸 Array Traversal
Use for or for-each loop:
```java
int[] arr = {10, 20, 30};
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}

// For-each loop
for (int num : arr) {
    System.out.println(num);
}

```
#### 🔸 Array vs ArrayList

| Feature     | Array                     | ArrayList                                      |
| ----------- | ------------------------- | ---------------------------------------------- |
| Fixed Size  | Yes                       | No (can grow/shrink)                           |
| Type        | Can store primitives      | Stores objects only (e.g. `Integer`)           |
| Performance | Faster                    | Slightly slower (dynamic resizing)             |
| Syntax      | `int[] arr = new int[5];` | `ArrayList<Integer> list = new ArrayList<>();` |
---
### ✅ 6. Methods
Methods are blocks of code that perform specific tasks. They improve code reusability.
___
#### 🔸 Defining and Calling Methods
```java
public class Main {
    static void greet() {
        System.out.println("Hello!");
    }

    public static void main(String[] args) {
        greet();  // calling the method
    }
}
```
#### 🔸 Method Overloading
Multiple methods with same name but different parameters:
```java
void greet() {
    System.out.println("Hello");
}

void greet(String name) {
    System.out.println("Hello " + name);
}
```
___
#### 🔸 return Keyword
Used to return a value from a method:
```java
int add(int a, int b) {
    return a + b;
}
```
#### 🔸 Pass-by-Value
Java uses pass-by-value, meaning copies of variables are passed to methods:
```java
void changeValue(int x) {
    x = 50;
}

int a = 10;
changeValue(a);
// a is still 10 (not changed)
```
For objects, the reference is passed by value, so internal fields can still be changed.
```java
void updateName(Person p) {
    p.name = "Alice";
}
```

# 2022~2023

### 1. Object-Oriented Programming / Java / Programming paradigms (25 marks)

#### (a) What is the output of the following Java statements: 

(i)

```java
SumList l1 = new SumList(2);
System.out.println(l1.toString(5));
```

**Output:**

```
2; 2; 4; 6; 10
```

(ii)

```java
SumList l2 = new SumList(3);
SumList l3 = l2.next().next();
l3.value = 7;
System.out.println(l3.prev.toString(6));
```

**Output:**

```
3; 7; 10; 17; 27; 44
```

(iii)

```java
System.out.println(l1.next().value * l3.next().next().value);
```

**Output:**

```
34
```

#### (b) Write an iterative method `toString` which also takes an int variable as input and generates the same output as before.

```java
public String toString(int n) {
    StringBuilder result = new StringBuilder();
    SumList current = this;
    for (int i = 0; i < n; i++) {
        if (i > 0) {
            result.append("; ");
        }
        result.append(current.value);
        current = current.next();
    }
    return result.toString();
}
```

#### (c) Write a `void setValue(int n)` method to update the value of the current object and all its successors as specified.

```java
public void setValue(int n) {
    this.value = n;
    if (this.prev != null) {
        this.prev.next = null;
        this.prev = null;
    }
    SumList current = this;
    while (current != null) {
        current.value = n;
        current = current.next;
    }
}
```

#### (d) 

(i) **Why does this not produce any syntax errors?**
Because the two methods `toString(int n)` and `toString()` are overloaded methods, having different parameter lists.

(ii)

```java
System.out.println(l1.toString());
```

**Output:**

```
StackOverflowError
```

The error occurs due to an infinite recursion in the `toString()` method, which keeps creating and trying to print new `IntList` elements when `next` is `null`.

### 2. Object-Oriented Programming/Java / Haskell Trees (25 marks)

#### (a) Write a data declaration for binary tree in Haskell.

```haskell
data BinaryTree a = Empty | Node a (BinaryTree a) (BinaryTree a)
```

#### (b) Write a Java class `MyBTreeNode` for binary tree nodes.

```java
public class MyBTreeNode extends AbstractTreeNode {
    private MyBTreeNode left;
    private MyBTreeNode right;

    public MyBTreeNode(int value) {
        super(value);
        this.left = null;
        this.right = null;
    }

    @Override
    public AbstractTreeNode[] getChildren() {
        return new AbstractTreeNode[]{left, right};
    }

    public MyBTreeNode getLeft() {
        return left;
    }

    public MyBTreeNode getRight() {
        return right;
    }

    public void setLeft(MyBTreeNode left) {
        this.left = left;
    }

    public void setRight(MyBTreeNode right) {
        this.right = right;
    }
}
```

#### (c) Revise your code of `MyBTreeNode` to ensure it works properly with `addChild`.

```java
public boolean addChild(AbstractTreeNode node) {
    if (node instanceof MyBTreeNode) {
        MyBTreeNode child = (MyBTreeNode) node;
        if (this.left == null) {
            this.left = child;
        } else if (this.right == null) {
            this.right = child;
        } else {
            return false; // Both children are already set
        }
        child.parent = this;
        return true;
    }
    return false;
}
```

#### (d) Write a Java method and a Haskell function to check if a given value exists in an integer binary tree.

**Java:**

```java
public boolean hasValue(int n) {
    Queue<MyBTreeNode> queue = new LinkedList<>();
    queue.add(this);
    while (!queue.isEmpty()) {
        MyBTreeNode current = queue.poll();
        if (current.getValue() == n) {
            return true;
        }
        if (current.getLeft() != null) {
            queue.add(current.getLeft());
        }
        if (current.getRight() != null) {
            queue.add(current.getRight());
        }
    }
    return false;
}
```

**Haskell:**

```haskell
hasValue :: BinaryTree Int -> Int -> Bool
hasValue Empty _ = False
hasValue (Node value left right) n
    | value == n = True
    | otherwise = hasValue left n || hasValue right n
```

---

# 2021~2022

### 1. Object-Oriented Programming / Java / Programming paradigms (25 marks)

#### (a) Which of these statements are true and which are false?

(i) An instance can be created from an abstract class.

- **False**

(ii) Multiple inheritance of interfaces is possible.

- **True**

(iii) A protected method in a class A can be accessed by a subclass of A.

- **True**

(iv) All classes and interfaces in Java are subclasses of the Object class.

- **True**

#### (b) Describe the four key principles of Object Oriented Programming.

1. **Encapsulation**: The bundling of data with the methods that operate on that data, restricting direct access to some of the object's components.
2. **Inheritance**: The mechanism by which one class can inherit the properties and behaviors of another class.
3. **Polymorphism**: The ability of different classes to be treated as instances of the same class through a common interface.
4. **Abstraction**: The concept of hiding the complex implementation details and showing only the necessary features of the object.

#### (c) Describe these two approaches to polymorphism in Java: Overloading and Overriding.

- **Overloading**: This occurs when two or more methods in the same class have the same name but different parameters. Example:

  ```java
  public class Example {
      public void display(int a) {
          System.out.println(a);
      }
      public void display(String b) {
          System.out.println(b);
      }
  }
  ```

- **Overriding**: This occurs when a subclass provides a specific implementation for a method that is already defined in its superclass. Example:

  ```java
  public class Animal {
      public void sound() {
          System.out.println("Animal makes a sound");
      }
  }
  
  public class Dog extends Animal {
      @Override
      public void sound() {
          System.out.println("Dog barks");
      }
  }
  ```

#### (d) Describe five key contrasts between these two pieces of code written in Java and Haskell.

**Java:**

```java
int[] x = new int[10];
x[0] = 1;
for (int i=0; i<x.length-1; i++)
    x[i+1] = x[i]*2;
```

**Haskell:**

```haskell
map (2^) [0..9]
```

**Contrasts:**

1. **Imperative vs Functional**: The Java code is imperative, specifying steps to change state, while the Haskell code is functional, describing a computation without state changes.
2. **Mutability vs Immutability**: Java uses a mutable array, whereas Haskell works with immutable lists.
3. **Explicit Loop vs Higher-Order Function**: Java uses an explicit `for` loop to iterate, while Haskell uses the higher-order function `map`.
4. **Initialization**: In Java, array elements must be initialized explicitly, whereas in Haskell, the list `[0..9]` is generated automatically.
5. **Conciseness**: Haskell’s code is more concise compared to the Java code.

### 2. Object-Oriented Programming / Java (25 marks)

#### (a) What is the output from executing the following sequence of code?

(i)

```java
IntList x1 = new IntList(4);
System.out.println(String.valueOf(x1.getValue() * x1.next().getValue()));
```

**Output:**

```
16
```

(ii)

```java
System.out.println(x1.toString(10));
```

**Output:**

```
4; 4; 4; 4; 4; 4; 4; 4; 4; 4
```

(iii)

```java
IntList x2 = new IntList(0);
IntList x3 = x2.next().next().next();
x3.setValue(5);
x3.next().next().setValue(8);
System.out.println(x2.toString(8));
```

**Output:**

```
0; 0; 0; 5; 5; 8; 8; 8
```

(iv)

```java
System.out.println(x3.previous().toString(2));
```

**Output:**

```
0; 5
```

#### (b) Provide the code for a subclass `IntListInc` of `IntList`.

```java
public class IntListInc extends IntList {
    private int inc;

    public IntListInc(int value, int inc) {
        super(value);
        this.inc = inc;
    }

    @Override
    public IntList next() {
        if (next == null) {
            next = new IntListInc(this.value + inc, inc);
            next.prev = this;
        }
        return next;
    }
}
```

#### (c)

(i) **Why does this not produce a syntax error?**
Because method overloading allows multiple methods with the same name but different parameter lists within the same class.

(ii)

```java
System.out.println(x1.toString());
```

**Output:**

```
StackOverflowError
```

The error occurs due to an infinite recursion in the `toString()` method, which keeps creating and trying to print new `IntList` elements when `next` is `null`.

#### (d) Write code using a `for` loop that takes an array `int[] ns` and constructs a new `IntList` object.

```java
public class IntListFromArray extends IntList {
    public IntListFromArray(int[] ns) {
        super(ns[0]);
        IntList current = this;
        for (int i = 1; i < ns.length; i++) {
            current.next = new IntList(ns[i]);
            current.next.prev = current;
            current = current.next;
        }
        for (int i = ns.length; i < 6; i++) {
            current.next = new IntList(0);
            current.next.prev = current;
            current = current.next;
        }
    }
}
```

Example usage:

```java
int[] ns = {5, 2, 6, 7};
IntList x5 = new IntList(ns[0]);
IntList current = x5;

for (int i = 1; i < ns.length; i++) {
    current.next = new IntList(ns[i]);
    current.next.prev = current;
    current = current.next;
}

for (int i = 0; i < 2; i++) {
    current.next = new IntList(0);
    current.next.prev = current;
    current = current.next;
}

System.out.println(x5.toString(6));
```

**Output:**

```
5; 2; 6; 7; 0; 0
```

---

# 2020~2021

### 1. Object-Oriented Programming/Java (25 marks)

#### (a) Compile-time error, run-time exception, and best practice issue.

**Line B:**

```java
Parent obj2 = new Parent();
```

- **Compile-time error**: None.
- **Runtime exception**: None.
- **Best practice issue**: None.

**Line C:**

```java
Parent obj3 = new Child();
```

- **Compile-time error**: None.
- **Runtime exception**: None.
- **Best practice issue**: None.

**Line D:**

```java
Child obj4 = new Parent(); 
```

- **Compile-time error**: Incompatible types: `Parent` cannot be converted to `Child`.

**Line E:**

```java
Child obj5 = (Child)obj2;
```

- **Compile-time error**: None.
- **Runtime exception**: ClassCastException at runtime as `obj2` is of type `Parent`.

**Line F:**

```java
Child obj6 = (Child)obj3;
```

- **Compile-time error**: None.
- **Runtime exception**: None, because `obj3` is of type `Child` at runtime.

**Line A**:

```java
void PrintData() { ... }
```

- **Best practice issue**: Missing `@Override` annotation to indicate method overriding.

#### (b) Output of `PrintData()` for each viable object created within the main method.

```java
obj1.PrintData(); // Output: "method of child class"
obj2.PrintData(); // Output: "method of parent class"
obj3.PrintData(); // Output: "method of child class"
obj4.PrintData(); // Not created due to compile-time error
obj5.PrintData(); // Runtime exception: ClassCastException
obj6.PrintData(); // Output: "method of child class"
```

#### (c) Parametric polymorphism

Parametric polymorphism allows methods to operate on objects of various types while providing compile-time type safety. It is achieved using generics.

**Example**:

```java
public class Box<T> {
    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}

Box<Integer> intBox = new Box<>();
intBox.set(123);
Integer value = intBox.get();
```

#### (d) Abstraction

**Abstraction** is the concept of hiding the complex implementation details and showing only the necessary features of an object.

- **Java Example**: Using abstract classes and interfaces to define a contract without implementation details.

  ```java
  abstract class Shape {
      abstract void draw();
  }
  
  class Circle extends Shape {
      void draw() {
          System.out.println("Drawing Circle");
      }
  }
  ```

- **Haskell Example**: Using type classes to define a contract.

  ```haskell
  class Shape a where
      draw :: a -> String
  
  data Circle = Circle
  instance Shape Circle where
      draw _ = "Drawing Circle"
  ```

### 2. Object-Oriented Programming/Java (25 marks)

#### (a) Exceptions in Java

- **Definition**: Exceptions are events that disrupt the normal flow of the program's instructions.

- **Causes**: Invalid user input, file not found, network connection failure, etc.

- **Unhandled example**: If not handled, the program terminates abruptly.

  ```java
  int a = 5 / 0; // Causes ArithmeticException if not handled
  ```

#### (b) Checked vs Unchecked Exceptions

- **Checked exceptions**: Must be declared in a method or constructor's `throws` clause. Example: `IOException`.
- **Unchecked exceptions**: Include `RuntimeException` and its subclasses. Example: `NullPointerException`.

#### (c) Immutable in Java

- **Definition**: Immutable objects cannot be modified after their creation.

- **Example**: The `String` class.

  ```java
  String s = "Hello";
  s.concat(" World");
  System.out.println(s); // Outputs "Hello"
  ```

- **Usefulness**: Simplifies concurrent programming, safer and easier to understand.

#### (d) Scanner class in Java

- **Function**: Used to read input from various sources (e.g., input streams, files).

- **Example**: Reading user input from the console.

  ```java
  Scanner scanner = new Scanner(System.in);
  System.out.print("Enter your name: ");
  String name = scanner.nextLine();
  System.out.println("Hello, " + name);
  ```

#### (e) Packages in Java

- **Definition**: A namespace for organizing classes and interfaces.
- **Usefulness**: Avoids name conflicts, organizes code logically, and controls access.

#### (f) Differences between `int` and `Integer`

- **`int`**: Primitive data type.
- **`Integer`**: Wrapper class for `int` that provides methods for converting and manipulating integers.
- **Benefits**:
  - `Integer` can be used in collections like `ArrayList`.
  - Provides utility methods (e.g., `parseInt`).

#### (g) Short commented program with interface and abstract class

```java
// Interface Animal with two methods
interface Animal {
    void eat();
    void move();
}

// Abstract class Fish implementing move method
abstract class Fish implements Animal {
    public void move() {
        System.out.println("I swim");
    }
}

// Subclass Piranha providing implementation for eat method
class Piranha extends Fish {
    public void eat() {
        System.out.println("I bite");
    }
}

// Main class to test the implementation
public class Main {
    public static void main(String[] args) {
        Piranha piranha = new Piranha();
        piranha.move(); // Outputs: I swim
        piranha.eat();  // Outputs: I bite
    }
}
```

---

# 2019~2020

### 1. Object-Oriented Programming/Java (25 marks)

#### (a) Explain, in fewer than 20 words, what it means to declare a method final.

A final method cannot be overridden by subclasses.

#### (b) Explain, in fewer than 20 words, what it means to declare a class final.

A final class cannot be subclassed or extended.

#### (c) Strings are immutable in Java. Explain what this means, give one benefit of this and explain why this is a benefit.

**Explanation**: Once created, the value of a String object cannot be changed.
**Benefit**: Thread safety.
**Why**: Immutable objects can be shared between threads without synchronization.

#### (d) What is constructor overloading in Java.

Defining multiple constructors in a class with different parameter lists.

#### (e) What is the difference between an inner class and a sub-class.

**Inner Class**: Defined within another class and has access to its members.
**Sub-Class**: Inherits from another class and can extend or modify its behavior.

#### (f) Briefly explain the difference between a syntax, runtime, and logical error in Java and how the compiler or JVM alerts you to these.

- **Syntax Error**: Violations of language rules, caught at compile-time.
- **Runtime Error**: Errors occurring during execution, such as exceptions.
- **Logical Error**: Errors in program logic, producing incorrect results without crashing, not directly detected by the compiler or JVM.

#### (g) Correct the syntax, runtime, and logical error in the given code.

**Original Code**:

```java
public class Rand2 {
    public static void main(String[] args) {
        double x, ratio;
        int plus = 0, minus = 0;
        
        for(int i=1; i<19; i++) {
            x = Math.random();
            if (x > 0.5) plus++;
            else minus++;
        }
        ratio = (double)plus / minus;
        System.out.println("ratio " + ratio);
    }
}
```

**Corrections**:

- Initialize `plus` and `minus` variables.
- Change `for(int i=1; i<19; i++)` to `for(int i=0; i<20; i++)` for 20 iterations.

### 2. Object-Oriented Programming/Java (25 marks)

#### (a) Give two similarities and two differences between interfaces and classes.

**Similarities**:

1. Both can contain methods.
2. Both can be used to define types.

**Differences**:

1. Interfaces cannot have instance fields; classes can.
2. Classes can have constructors; interfaces cannot.

#### (b) What does method overriding do? Give a simple coded example.

Method overriding allows a subclass to provide a specific implementation for a method already defined in its superclass.

**Example**:

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
```

#### (c) Class diagram

**Description**:

- Vehicle class: fields for color, maxSpeed, methods to set these fields, and a method to display them.
- Engine class: methods `start` and `stop`.
- Helicopter class: extends Vehicle, uses Engine.

```plaintext
+----------------+      +--------------+
|  Vehicle       |      |  Engine      |
|----------------|      |--------------|
| - color: String|      | +start()     |
| - maxSpeed: int|      | +stop()      |
|----------------|      +--------------+
| +setColor()    |
| +setMaxSpeed() |
| +display()     |
+----------------+
        ^
        |
+-----------------+
|  Helicopter     |
|-----------------|
| - engine: Engine|
|-----------------|
| +start()        |
| +stop()         |
+-----------------+
```

#### (d) Write the three required classes

**Vehicle.java**:

```java
public class Vehicle {
    private String color;
    private int maxSpeed;

    public void setColor(String color) {
        this.color = color;
    }

    public void setMaxSpeed(int maxSpeed) {
        this.maxSpeed = maxSpeed;
    }

    public void display() {
        System.out.println("Vehicle Colour is " + color + " and Max speed is " + maxSpeed);
    }
}
```

**Engine.java**:

```java
import java.time.LocalDateTime;

public class Engine {
    public void start() {
        System.out.println("Engine started at " + LocalDateTime.now());
    }

    public void stop() {
        System.out.println("Engine stopped at " + LocalDateTime.now());
    }
}
```

**Helicopter.java**:

```java
public class Helicopter extends Vehicle {
    private Engine engine = new Engine();

    public void start() {
        engine.start();
    }

    public void stop() {
        engine.stop();
    }
}
```

**HeliDemo.java**:

```java
public class HeliDemo {
    public static void main(String[] args) {
        Helicopter myHeli = new Helicopter();
        myHeli.setColor("Red");
        myHeli.setMaxSpeed(200);
        myHeli.display();
        myHeli.start();
    }
}
```

#### (e) Benefits of using the object-oriented approach

1. **Reusability**: Code can be reused through inheritance and composition, reducing redundancy.
2. **Maintainability**: Code is organized into classes, making it easier to maintain and extend.

### 3. Object-Oriented Programming/Java (25 marks)

#### (a) Explain, in fewer than 20 words, what it means to declare a method final.

A final method cannot be overridden by subclasses.

#### (b) Explain, in fewer than 20 words, what it means to declare a class final.

A final class cannot be subclassed or extended.

#### (c) Strings are immutable in Java. Explain what this means, give one benefit of this and explain why this is a benefit.

**Explanation**: Once created, the value of a String object cannot be changed.
**Benefit**: Thread safety.
**Why**: Immutable objects can be shared between threads without synchronization.

#### (d) What is constructor overloading in Java.

Defining multiple constructors in a class with different parameter lists.

#### (e) What is the difference between an inner class and a sub-class.

**Inner Class**: Defined within another class and has access to its members.
**Sub-Class**: Inherits from another class and can extend or modify its behavior.

#### (f) Briefly explain the difference between a syntax, runtime, and logical error in Java and how the compiler or JVM alerts you to these.

- **Syntax Error**: Violations of language rules, caught at compile-time.
- **Runtime Error**: Errors occurring during execution, such as exceptions.
- **Logical Error**: Errors in program logic, producing incorrect results without crashing, not directly detected by the compiler or JVM.

#### (g) Correct the syntax, runtime, and logical error in the given code.

**Original Code**:

```java
public class Rand2 {
    public static void main(String[] args) {
        double x, ratio;
        int plus = 0, minus = 0;
        
        for(int i=1; i<19; i++) {
            x = Math.random();
            if (x > 0.5) plus++;
            else minus++;
        }
        ratio = (double)plus / minus;
        System.out.println("ratio " + ratio);
    }
}
```

**Corrections**:

- Initialize `plus` and `minus` variables.
- Change `for(int i=1; i<19; i++)` to `for(int i=0; i<20; i++)` for 20 iterations.

---

# 2018~2019

### 1. Object-Oriented Programming/Java (25 marks)

#### (a) Name and briefly describe 4 primitive numeric data types.

1. **byte**: 8-bit signed integer.
2. **short**: 16-bit signed integer.
3. **int**: 32-bit signed integer.
4. **double**: 64-bit floating-point number.

#### (b) Fill in the missing lines to complete the program and give the desired output.

**Program**:

```java
public class Exam1 {
    public static <E> void printArray(E[] inputArray) {
        for(E element : inputArray) {
            System.out.printf("%s ", element);
        }
        System.out.println();
    }

    public static void main(String args[]) {
        Integer[] intArray = {1, 2, 3, 4, 5}; // Define an integer array
        Character[] charArray = {'H', 'E', 'L', 'L', 'O', '0'}; // Define a character array
        printArray(intArray); // Pass integer array to method
        printArray(charArray); // Pass character array to method
    }
}
```

**Output**:

```
1 2 3 4 5 
H E L L O 0 
```

#### (c) What key feature of Object Orientation does the program in the previous question exemplify and why?

**Feature**: Generics.
**Why**: It allows methods to operate on different types without specifying the exact type.

#### (d) Describe, with examples, 3 different types of polymorphism.

1. **Compile-time polymorphism (Method Overloading)**:

   ```java
   class Example {
       void display(int a) {
           System.out.println(a);
       }
       void display(String a) {
           System.out.println(a);
       }
   }
   ```

2. **Runtime polymorphism (Method Overriding)**:

   ```java
   class Parent {
       void display() {
           System.out.println("Parent");
       }
   }
   class Child extends Parent {
       @Override
       void display() {
           System.out.println("Child");
       }
   }
   ```

3. **Subtype polymorphism (Interfaces)**:

   ```java
   interface Animal {
       void sound();
   }
   class Dog implements Animal {
       public void sound() {
           System.out.println("Bark");
       }
   }
   ```

#### (e) Briefly, what is method overriding and method overloading and whether they are compile or runtime concepts.

- **Method Overriding**: Redefining a method in a subclass. **Runtime concept**.
- **Method Overloading**: Defining multiple methods with the same name but different parameters. **Compile-time concept**.

#### (f) Discuss briefly why Java is generally seen as a safer language than C.

Java has built-in memory management with garbage collection, bounds checking, and lacks direct memory manipulation like pointers in C.

#### (g) What is the difference between an inner class and a sub-class.

- **Inner Class**: Defined within another class, has access to its enclosing class's members.
- **Sub-Class**: Inherits from another class, extending or modifying its behavior.

### 2. Object-Oriented Programming/Java (25 marks)

#### (a) What is Java bytecode. Discuss a possible advantage and possible disadvantage that this gives Java over traditional programming language implementations.

**Java Bytecode**: Intermediate code executed by the Java Virtual Machine (JVM).

**Advantage**: Platform independence.
**Disadvantage**: Slower execution compared to native code due to interpretation or JIT compilation.

#### (b) What is the output from the following code.

**Code**:

```java
public class Test2 {
    public static void main(String args[]) {
        int n;
        try {
            n = calc();
            System.out.println(n);
        } catch(Exception e) {
            System.out.println("Error");
        }
        try {
            n = calculate();
            System.out.println(n);
        } catch(Exception e) {
            System.out.println("Error");
        }
    }
    static int calculate() {
        return (2/3);
    }
    static int calc() {
        return (2/0);
    }
}
```

**Output**:

```
Error
0
```

#### (c) What is the 'final' keyword used for in Java, give examples of its use.

**Usage**:

1. **Final variable**: Value cannot be changed.

   ```java
   final int CONSTANT = 10;
   ```

2. **Final method**: Cannot be overridden.

   ```java
   class Parent {
       final void display() {
           System.out.println("Parent");
       }
   }
   ```

3. **Final class**: Cannot be subclassed.

   ```java
   final class FinalClass {}
   ```

#### (d) The following code fails to compile. What operator is missing and what will the output be once the operator is correctly inserted, compiled and executed.

**Original Code**:

```java
public class Calculate {
    int num = 10;
    public void calc(int num) {
        this.num = num * 8;
    }
    public void printNum() {
        System.out.println(num);
    }
    public static void main(String[] args) {
        Calculate obj = new Calculate();
        obj.calc(2);
        obj.printNum();
    }
}
```

**Missing Operator**: `new`
**Corrected Code**:

```java
public class Calculate {
    int num = 10;
    public void calc(int num) {
        this.num = num * 8;
    }
    public void printNum() {
        System.out.println(num);
    }
    public static void main(String[] args) {
        Calculate obj = new Calculate();
        obj.calc(2);
        obj.printNum();
    }
}
```

**Output**:

```
16
```

#### (e) Examine the following code, write the 4 lines of output, giving the missing text.

**Code**:

```java
class People {
    public int age;
    People(int age) { this.age = age; }
}

public class TestPeople {
    static void change1(People p) {
        System.out.println("(1) " + p + " age: " + p.age);
        People newP = new People(p.age);
        p = newP;
        System.out.println("(2) " + p + " age: " + p.age);
    }
    static void change2(People p) {
        System.out.println("(3) " + p + " age: " + p.age);
        p.age += 10;
        System.out.println("(4) " + p + " age: " + p.age);
    }
    public static void main(String[] args) {
        People p = new People(25);
        change2(p);
        change1(p);
    }
}
```

**Output**:

```
(3) People@<hashcode1> age: 25
(4) People@<hashcode1> age: 35
(1) People@<hashcode1> age: 35
(2) People@<hashcode2> age: 35
```

#### (f) Discuss the main concept the previous question highlights.

**Concept**: Object references and immutability.

- **Explanation**: Changes to the object's fields persist outside the method (change2), but reassigning the object reference (change1) does not affect the original reference.

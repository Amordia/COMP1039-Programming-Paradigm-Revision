## Principles of OOP

### Encapsulation

**Description**: Encapsulation is an OOP principle that **restricts direct access to an object**'s data and methods, providing controlled access through methods. It helps to **protect the integrity of the data and the complexity of the operations** performed on the data.

**Java Example**:

```java
public class Person {
    private String name;  // Private variable, encapsulated within the class

    public String getName() {
        return name;  // Public method to access private variable
    }

    public void setName(String name) {
        this.name = name;  // Public method to modify private variable
    }
}
```

#### Access Modifiers

[Jump to Detail: Access Modifiers](#Detail-Access-Modifiers)

#### Package

[Jump to Detail: Package](#Detail-Package)

#### Static vs Non-static

[Jump to Detail: Static vs Non-static](#Detail-Static-vs-Non-static)

#### Keywords: `this`, `super`

[Jump to Detail: Keywords: `this`, `super`](#Detail: Keywords: `this`, `super`)

#### Inner Class

[Jump to Detail: Inner Class](#Detail-Inner-Class)

---

### Inheritance

**Description**: Inheritance is a mechanism where **a new class derives properties and behaviors (methods) from an existing class**. In Java, inheritance is declared using the `extends` keyword.

**Java Example**:

```java
public class Animal {
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

public class Dog extends Animal {
    public void bark() {
        System.out.println("The dog barks.");
    }
}
```

#### Superclass and Subclass

**Description**: In Java, a *superclass* (or base class) is a class that is extended by another class (subclass). The *subclass* inherits fields and methods from the superclass, enabling code reuse and polymorphism.

**Java Example**:

```java
public class Animal {  // Superclass
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

public class Dog extends Animal {  // Subclass
    public void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.eat();  // Inherited method
        myDog.bark(); // Subclass method
    }
}
```

#### Keywords: `this`, `super`

[Jump to Detail: Keywords: `this`, `super`](#Detail: Keywords: `this`, `super`)

#### Abstract Class and Interface

[Jump to Detail: Abstract Class and Interface](#Detail-Abstract-Class-and-Interface)

----

### Abstraction

**Description**: Abstraction is an OOP concept that focuses on **exposing essential features of an object** while **hiding internal details**. It is typically accomplished through **abstract classes and interfaces**.

**Java Example**:

```java
public abstract class Shape {
    abstract void draw();  // Abstract method
}

public class Circle extends Shape {
    void draw() {
        System.out.println("Drawing a circle.");
    }
}

public interface Drawable {
    void draw();
}
```

#### Abstract vs Concrete

[Jump to Detail: Abstract vs Concrete](#Detail-Abstract-vs-Concrete)

#### Abstract Class and Interface

[Jump to Detail: Abstract Class and Interface](#Detail-Abstract-Class-and-Interface)

#### Keywords: `this`, `super`

[Jump to Detail: Keywords: `this`, `super`](#Detail: Keywords: `this`, `super`)

---

### Polymorphism

**Description**: Polymorphism in Java **allows methods to do different things based on the object's class that implements these methods**. It can be achieved by method *overriding* (where a **subclass provides a specific implementation of a method that is already defined in its superclass**) and method *overloading* (where multiple **methods have the same name but different parameters within the same class**).

**Java Example**:

```java
// Polymorphism through overriding
public class Animal {
    public void sound() {
        System.out.println("Some sound");
    }
}

public class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Bark");
    }
}

// Polymorphism through overloading
public class Display {
    public void show(int a) {
        System.out.println("Integer: " + a);
    }

    public void show(String b) {
        System.out.println("String: " + b);
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();
        Animal myDog = new Dog();
        Display myDisplay = new Display();

        myAnimal.sound(); // Outputs "Some sound"
        myDog.sound();    // Outputs "Bark", demonstrating overriding

        myDisplay.show(123);      // Outputs "Integer: 123", demonstrating overloading
        myDisplay.show("Hello");  // Outputs "String: Hello", demonstrating overloading
    }
}
```

#### Override vs Overload

[Jump to Detail: Override vs Overload](#Detail-Override-vs-Overload)

#### Generic Data Type

[Jump to Detail: Generic Data Type](#Detail-Generic-Data-Type)

---

---

### Concept Details:

#### Detail: Access Modifiers

**Description**: Access modifiers in Java define the **accessibility of classes, methods, and other members**. They are key in encapsulation. The main types are `private`, `public`, `protected`, and package-private (no explicit modifier).

**Java Example**:

```java
public class AccessExample {
    private int a;  // Accessible only within the class
    public int b;   // Accessible from any other class
    protected int c; // Accessible within the same package or subclasses
    int d;          // Package-private, accessible within the same package
}
```

#### Detail: Package

**Description**: A package in Java is **a namespace that organizes a set of related classes and interfaces**. It helps in **avoiding name conflicts and can control access** via package-private visibility.

**Java Example**:

```java
package com.example.utilities;  // Declaring a package

public class Utility {
    // Class content
}
```

#### Detail: Static vs Non-static

**Description**: In Java, `static` members **belong to the class rather than any instance**, **accessible without creating an instance** of the class. Non-static members, however, **belong to specific instances of a class**.

**Java Example**:

```java
public class MyClass {
    static int staticVar = 100;  // Static variable
    int instanceVar = 50;        // Non-static variable

    public static void staticMethod() {
        System.out.println("This is a static method.");
    }

    public void instanceMethod() {
        System.out.println("This is an instance method.");
    }
    
    public static voiod main(String[] args) {
        System.out.println("The value of staticVar is: " + staticVar);
        staticMethod();
        
        MyClass obj = new Myclass();
        System.out.println("The value of instanceVar is: " + instanceVar);
        obj.instanceMethod();
    }
}
```

#### Override vs OverloadDetail: Keywords: `this`, `super`

**Description**: `this` refers to the **current object instance**, used to access **members or constructors within the same class**. `super` refers to the superclass, used to **access superclass members or constructors**.

**Java Example**:

```java
public class Animal {
    String name;
    
    public Animal (string name) {
        this.name = name;
    }
    
    public void eat() {
        System.out.println(name + "is eating.");
    }
}

public class Dog extends Animal {
    int age;
    
    public Dog(String name, int age){
    	super(name); // Call the parent class constractor
        this.age = age;
    }
    
    public void display() {
        System.out.println("Name: " + this.name);
        System.out.println("Age: " + this.age);
        super.eat(); // Call the method of the parent class
    }
}

public calss Main {
    public static void main(String[] args){
        Dog dog = new Dog("Buddy", 3);
        dog.display();
    }
}
```

#### Detail: Inner Class

**Description**: Inner classes are **defined within another class** and can **access its enclosing class's members**. They are useful for logically grouping classes that are only used in one place. Inner classes can have any access modifiers.

**Java Example**:

```java
public class EnclosingClass {
    private in data;
    
    public EnclosingClass(int data) {
        this.data = data;
    }
    
    // InnerClass only used the EnclosingClass
    private class innerClass {
        public void display() {
            System.out.println("Data from EnclosingClass:" + data);
        }   
    }
    
    // The Outer Class provide the public method to access Inner Class
    public void accessInnerClass() {
        InnerClass inner = new InnerClass();
        inner.display();
    }
}

public class Main {
    public static void main(String[] args) {
        EnclosingClass enclosing = new EnclosingClass(10);
        enclosing.accessInnerClass();
    }
}
```

#### Detail: Abstract vs Concrete

**Description**: An abstract class **cannot be instantiated** and **may contain abstract methods without implementation**. Concrete classes are normal classes that **can be instantiated** and do **not contain any abstract methods**.

**Java Example**:

```java
public abstract class Shape {
    public abstract double calculateArea();
}

public class Rectangle extends Shape {
    private double length;
    private double width;
    
    public Rectangle(double length, double width) {
        this.length = length;
        this width = width;
    }
    
    @Override
    public double calculateArea() {
        return length * width;
    }
}

public class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius *radius;
    }
}
```

#### Detail: Abstract Class and Interface

**Description**: An *abstract class* in Java is a class that **cannot be instantiated** and may **contain abstract methods without implementations**. *Interfaces* **define a contract for what a class can do**, without implementing any behavior. Classes can **implement multiple interfaces** but **extend only one abstract class**.

**Java Example**:

```java
public abstract class Vehicle {  // Abstract class
    abstract void go();  // Abstract method with no implementation
}

interface Movable {  // Interface
    void move();  // Interface method (implicitly public and abstract)
}

public class Car extends Vehicle implements Movable {  // Extends abstract class and implements interface
    @Override
    public void go() {
        System.out.println("The car goes.");
    }

    @Override
    public void move() {
        System.out.println("The car moves forward.");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.go();   // From abstract class
        myCar.move(); // From interface
    }
}
```

#### Detail: Override vs Overload

**Description**: *Overriding* is a feature that allows a subclass to provide a specific implementation of a method that is already provided by its superclass. This is used for runtime polymorphism. *Overloading*, on the other hand, allows a class to have more than one method having the same name, if their parameter lists are different. This is **used for compile-time polymorphism**.

**Java Example**:

```java
// Overriding Example
public class Bird {
    public void sing() {
        System.out.println("Bird sings");
    }
}

public class Sparrow extends Bird {
    @Override
    public void sing() {
        System.out.println("Sparrow sings chirp chirp");
    }
}

// Overloading Example
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Bird myBird = new Sparrow();  // Polymorphic declaration
        myBird.sing();  // Outputs "Sparrow sings chirp chirp" due to overriding

        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 3));        // Uses int add(int, int)
        System.out.println(calc.add(5.0, 3.0));    // Uses double add(double, double) due to overloading
    }
}
```

#### Detail: Generic Data Type

**Description**: Generics **enable types (classes and interfaces) to be parameters** when defining classes, interfaces, and methods. This allows a type or method to operate on objects of various types while **providing compile-time type safety**.

**Java Example**:

```java
public class GenericBox<T> {
    private T t; // T stands for "Type"

    public void set(T t) {
        this.t = t;
    }

    public T get() {
        return t;
    }

    public static void main(String[] args) {
        GenericBox<Integer> integerBox = new GenericBox<>();
        integerBox.set(10); // Autoboxing of int to Integer
        System.out.println(integerBox.get());
    }
}
```

---



---

## Other Concepts

### Primitive type vs OO type
#### Call by value
- **Explanation**: Java passes primitives by value, meaning a copy of the variable is made.
- **Example**:
  ```java
  public static void main(String[] args) {
      int x = 5;
      increment(x);
      System.out.println(x); // Prints: 5
  }
  
  public static void increment(int number) {
      number++;
  }
  ```

#### Call by reference
- **Explanation**: Java passes objects by reference, meaning the method can affect the object's state.
- **Example**:
  ```java
  public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Hello");
      appendExclamation(sb);
      System.out.println(sb); // Prints: Hello!
  }
  
  public static void appendExclamation(StringBuilder s) {
      s.append("!");
  }
  ```

#### Data wrapper
- **Explanation**: Wrapper classes turn primitives into objects, enabling methods and storage in collections.
- **Example**:
  ```java
  Integer myInt = Integer.valueOf(10);
  Double myDouble = Double.valueOf(5.99);
  ```

### Loops
#### For
- **Example**:
  ```java
  for (int i = 0; i < 3; i++) {
      System.out.println("i = " + i);
  }
  ```

#### While
- **Example**:
  ```java
  int i = 0;
  while (i < 3) {
      System.out.println("i = " + i);
      i++;
  }
  ```

#### Foreach
- **Example**:
  ```java
  String[] names = {"Alice", "Bob", "Charlie"};
  for (String name : names) {
      System.out.println(name);
  }
  ```

#### Label, break, continue
- **Example**:
  ```java
  outer: for (int i = 0; i < 3; i++) {
      for (int j = 0; j < 3; j++) {
          if (j == 1) continue outer;
          if (i == 2) break outer;
          System.out.println("i = " + i + ", j = " + j);
      }
  }
  ```

### If-then-else, Switch
#### If-then-else
- **Example**:
  ```java
  int number = 10;
  if (number > 0) {
      System.out.println("Positive");
  } else {
      System.out.println("Non-positive");
  }
  ```

#### Switch
- **Example**:
  ```java
  int month = 4;
  switch (month) {
      case 1: System.out.println("January"); break;
      case 4: System.out.println("April"); break;
      default: System.out.println("Other Month");
  }
  ```

### Recursive Call in Java
- **Example**:
  ```java
  public static int factorial(int n) {
      if (n <= 1) return 1;
      return n * factorial(n - 1);
  }
  ```

### Generic Data Type
- **Example**:
  ```java
  public class GenericBox<T> {
      private T t;
  
      public void set(T t) {
          this.t = t;
      }
  
      public T get() {
          return t;
      }
  }
  ```

### Input and Output
#### Stream: Byte stream and Character stream
- **Explanation**: Byte streams handle I/O of raw bytes, while character streams handle I/O of characters.
- **Example**:
  ```java
  try (FileInputStream in = new FileInputStream("data.bin");
       FileOutputStream out = new FileOutputStream("data.copy.bin")) {
      int byteData;
      while ((byteData = in.read()) != -1) {
          out.write(byteData);
      }
  } catch (IOException e) {
      e.printStackTrace();
  }
  ```

#### BufferedReader and Scanner
- **Example**:
  ```java
  try (Scanner scanner = new Scanner(System.in)) {
      while (scanner.hasNext()) {
          System.out.println(scanner.nextLine());
      }
  }
  ```

#### FileReader and FileWriter
- **Example**:
  ```java
  try (FileReader fr = new FileReader("text.txt");
       FileWriter fw = new FileWriter("newText.txt")) {
      int c;
      while ((c = fr.read()) != -1) {
          fw.write(c);
      }
  } catch (IOException e) {
      e.printStackTrace();
  }
  ```

### Exceptions
#### Checked vs Unchecked
- **Explanation**: Checked exceptions must be handled or declared, whereas unchecked do not need explicit handling.
- **Example**:

  ```java
  // Checked exception needs to be declared or handled
  public void readFile() throws IOException {
      FileInputStream file = new FileInputStream("nonexistent.txt");
      file.close();
  }

  // Unchecked exceptions can be thrown without declaration
  public void divideByZero() {
      int i = 1 / 0;
  }
  ```

#### Try and Catch
- **Example**:
  
  ```java
  try {
      int[] numbers = new int[5];
      System.out.println(numbers[5]);
  } catch (ArrayIndexOutOfBoundsException e) {
      System.out.println("Index out of bounds!");
  }
  ```

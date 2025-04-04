Object Oriented Programming is a programming paradigm that organizes data and behaviors into reusable and self-contained units called objects.

# Class

> A blueprint or template for creating objects.

```java
public class Person {
    // Attributes (instance variables)
    String name;
    int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Method
    public void introduce() {
        System.out.println("Hello, I'm " + name + " and I'm " + age + " years old.");
    }
}
```

# Object

> Instance created from a class

```java
Person person1 = new Person("Alice", 30);
```

# Interface

> A blueprint for a class that defines a set of methods (function signatures) that must be implemented by any concrete class that implements the interface

```java
public interface Drawable {
    void draw();
}
```

# Class implements Interface

> 'Circle implements Drawable' it means that the Circle class is declaring that it will adhere to a contract defined by the Drawable interface = It agrees to provide concrete implementations for all the methods declared in that interface.

```java
// Interface representing drawable objects
public interface Drawable {
    void draw();
}

// Class implementing the Drawable interface
public class Circle implements Drawable {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a circle with radius " + radius);
    }
}
```

# 4 fundamental principles of OOP

- Inheritence
- Polymorphism
- Encapsulation
- Abstraction

## Inheritence

> Child inherits parent's properties and methods ("is a" relationship)

```java
public class Student extends Person {
    String studentId;

    public Student(String name, int age, String studentId) {
        super(name, age); // Use parent contructor
        this.studentId = studentId;
    }
}
```

## Polymorphism

> "many forms" in OOP

```java
// Shape is an abstract class or interface with a draw method.
interface Shape {
    void draw();
}

// Circle is a concrete class that implements the Shape interface.
class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle.");
    }
}

// Rectangle is a concrete class that implements the Shape interface.
class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle.");
    }
}

```

Can just use their abstract type "Shape" instead of actual Shape

```java
public class PolymorphismExample {
    public static void main(String[] args) {
        // Create instances of Circle and Rectangle.
        Shape circle = new Circle();
        Shape rectangle = new Rectangle();

        // Use polymorphism to call the draw method on both objects.
        circle.draw();    // Output: "Drawing a circle."
        rectangle.draw(); // Output: "Drawing a rectangle."

        // You can store different shapes in an array or collection and still call draw.
        Shape[] shapes = new Shape[]{circle, rectangle};
        for (Shape shape : shapes) {
            shape.draw();
        }
    }
}

```

## Encapsulation

> Bundle data of object into a single unit "class" and restrict access to internal state / data of object

More controlled access to state of object through getters and setters

```java
public class Person {
    // Private instance variables (attributes)
    private String name;
    private int age;

    // Constructor to initialize the person's name and age
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    //Public getters and setters ...
}
```

```java
public class EncapsulationExample {
    public static void main(String[] args) {
        // Create a Person object
        Person person = new Person("Alice", 30);

        // Access and modify the person's data using getters and setters
        System.out.println("Name: " + person.getName()); // Accessing the name
        System.out.println("Age: " + person.getAge());   // Accessing the age

        person.setName("Bob");  // Modifying the name
        person.setAge(25);      // Modifying the age

        System.out.println("Updated Name: " + person.getName()); // Accessing the updated name
        System.out.println("Updated Age: " + person.getAge());   // Accessing the updated age
    }
}
```

## Abstraction

> Simplifying complex systems by focusing on what an object does (its behaviors) while hiding how it does it (implementation details).

eg. A Shape interface defines methods like draw() and resize() without specifying how each shape is drawn or resized.

```java
// Abstract class
public abstract class Shape {
    // Concrete method defined in the abstract class
    public void displayInfo() {
        System.out.println("This is a shape.");
    }

    // Just come up with method , dont need to care about implementation cause that is handled by subclasses
    public abstract double area();
}

// Concrete subclass
public class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    // Implementing the abstract method from the abstract class
    @Override
    public double area() {
        return Math.PI * radius * radius;
    }

    // New method specific to the Circle class
    public void describe() {
        System.out.println("This is a circle with radius " + radius);
    }
}

public class Main {
    public static void main(String[] args) {
        Circle circle = new Circle(5.0);

        // Using methods from the abstract class
        circle.displayInfo();  // Output: "This is a shape."
        double circleArea = circle.area();

        // Using the subclass-specific method
        circle.describe();     // Output: "This is a circle with radius 5.0"
    }
}
```

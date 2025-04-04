# Implicit type casting

```java
int intValue = 10;
double doubleValue = intValue; // Implicit casting from int to double
```

# Explicit type casting

```java
double doubleValue = 10.5;
int intValue = (int) doubleValue; // Explicit casting from double to int

```

# Casting in classes

```java
class Animal { /* ... */ }
class Dog extends Animal { /* ... */ }

Animal animal = new Dog(); // Implicit casting (upcasting)
Dog dog = (Dog) animal;    // Explicit casting (downcasting)
```

# Order of data type from smallest to largest

--Implicit Casting (Widening)-->

byte, short, char, int, long, float, double

<--Explicit Casting (Narrowing)--

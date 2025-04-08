# Primitive data types

Store actual data

```java
byte myByte = 42;       // 8-bit signed integer (-128 to 127)
short myShort = 1000;   // 16-bit signed integer (-32,768 to 32,767)
int myInt = 12345;      // 32-bit signed integer
long myLong = 123456789L;  // 64-bit signed integer
float myFloat = 3.14f;  // 32-bit floating-point number (limited precision)
double myDouble = 3.14159265359;  // 64-bit floating-point number (higher precision)
char myChar = 'A';      // 16-bit Unicode character
boolean isTrue = true;  // Represents true or false
```

# Reference data types

Store references (memory addresses) to objects rather than storing the actual data

```java
String myString = "Hello, World!";  // A sequence of characters (string)
int[] intArray = {1, 2, 3, 4, 5};  // An array of integers
String[] stringArray = {"apple", "banana", "cherry"};  // An array of strings

class Person {  // Custom class definition
    String name;
    int age;
}

Person personObject = new Person();  // An instance of a custom class
personObject.name = "John";
personObject.age = 30;

import java.util.ArrayList;  // Importing standard library classes
import java.util.HashMap;
import java.util.HashSet;

ArrayList<Integer> list = new ArrayList<>();  // A dynamic array of integers
HashMap<String, Integer> map = new HashMap<>();  // A key-value map
HashSet<String> set = new HashSet<>();  // A set of unique elements
```

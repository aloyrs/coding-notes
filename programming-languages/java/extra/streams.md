Java Streams are a powerful and flexible abstraction for processing sequences of data

# Stream source

> Collections, Arrays, or I/O channels, etc.

# Intermediate Operations

> To manipulate the data in stream but not return anything

Examples :

- filter()
- map()
- sort()

# Terminal Operations

> Stop stream processing and return values from the stream

Examples :

- forEach()
- toArray()
- reduce()
- min() / max()

# Example

```java
List<String> fruits = Arrays.asList("apple", "banana", "cherry", "date", "elderberry");

List<String> filteredAndMappedFruits = fruits.stream()
        .filter(fruit -> fruit.length() > 5) // Intermediate Operation
        .map(fruit -> fruit.toUpperCase()) // Intermediate Operation
        .toList(); // Terminal Operation

System.out.println(filteredAndMappedFruits); // [BANANA, CHERRY, ELDERBERRY]
```

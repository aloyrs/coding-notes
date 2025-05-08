# When to use functional programming paradigm?

Use functional programming when you want to write cleaner, more concise code that focuses on what to do rather than how to do it, especially for processing collections or streams.

# Intermediate Operations (lazy)

These are lazy operations that return a new stream and are executed only when a terminal operation is invoked.

- `filter(Predicate)` – Keeps elements that match a condition
- `map(Function)` – Transforms each element
- `flatMap(Function)` – Flattens nested structures (e.g., Stream of Lists)

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        List<Integer> evensTimesTen = numbers.stream()
                .filter(n -> n % 2 == 0)    // intermediate: keep even numbers
                .map(n -> n * 10)           // intermediate: multiply each by 10
                .collect(Collectors.toList()); // terminal: trigger processing

        System.out.println(evensTimesTen); // Output: [20, 40, 60]
```

# Terminal Operations (Eager)

These trigger the stream pipeline and produce a result or side effect.

- `collect(Collectors.toList())` – Collects the result into a list
- `forEach(Consumer)` – Performs an action for each element
- `reduce(...)` – Reduces all elements into a single result

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4);

        int product = numbers.stream()
                .reduce(1, (a, b) -> a * b);  // terminal: multiply all numbers

        System.out.println("Product: " + product); // Output: Product: 24
```

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        names.stream()
             .forEach(name -> System.out.println("Hello " + name)); // terminal: print each

```

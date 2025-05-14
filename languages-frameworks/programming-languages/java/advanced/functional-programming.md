# Functional Programming

Pure functional programming follows these principles:

- No internal state or side effects

- Uses pure functions (same input → same output)

- Emphasizes higher-order functions (functions that take or return other functions)

"Functional programming is about writing functions that take inputs and return outputs without changing anything outside the function — no modifying global variables, just working with the arguments passed in."

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

# Function

.andThen

.compose

.apply

```java
// 1 arguement 1 output
Function<Integer,Integer> incrementBy1 = num -> num + 1;
Function<Integer,Integer> multiplyBy2 = num -> num * 2;

int incrementThenMultiply = incrementBy1.andThen(multiplyBy2).apply(5);
System.out.println(incrementThenMultiply); // Output: 12 , (5+1)*2

int multiplyThenIncrement = incrementBy1.compose(multiplyBy2).apply(5);
System.out.println(multiplyThenIncrement); // Output: 11 , (5*2)+1
```

```java
// 2 arguement 1 output
BiFunction<Integer,Integer,Integer> doubleOfSum = (num1,num2) -> (num1+num2)*2 ;
System.out.println(doubleOfSum.apply(2,3));
```

# Consumer

.accept

```java
List<Integer> nums = Arrays.asList(1,2,3,4,5,6,7,8,9);

Consumer<Integer> consumerInt = num -> System.out.println(num + 2);
consumerInt.accept(1);
```

```java
BiConsumer<Integer,Integer> outputSum = (num1,num2) -> System.out.println(num1+num2);
outputSum.accept(5,4); // 9
```

Can be used as a callback too!

# Predicate

Returns a boolean

```java
List<Integer> nums = Arrays.asList(1,2,3,4,5,6,7,8,9);
Predicate<Integer> divisibleByTwoPredicate = num -> num%2 == 0;
nums.stream().filter(divisibleByTwoPredicate).forEach(System.out::println);
```

# Supplier

Supplier is good because it lets you defer the creation of a value until it's actually needed, saving resources and improving efficiency.

"You want to define the logic now, but only execute it later, possibly under certain conditions."

```java
import java.util.function.*;

public class Main {

    public static String expensiveMethod(){
        return "super_expensive_text";
    }
    public static void main(String[] args) {

        Supplier<String> prepareExpensiveMethod = () -> expensiveMethod();

        // ...do others

        String expensiveText = prepareExpensiveMethod.get();
        System.out.println(expensiveText); //super_expensive_text

    }
}
```

# Optionals

.isPresent

.orElseThrow

Some functions will return a `Optional` object which means something or nothing.

Or we can use Optional to avoid `NullPointerException`

```java
String name = Optional.ofNullable(getName()).orElse("Default Name");
```

# Combinator pattern in functional programming

```java
import java.util.function.Function;

// A simple User class
class User {
    String name;
    String email;

    User(String name, String email) {
        this.name = name;
        this.email = email;
    }
}

// A result type to hold validation results
enum ValidationResult {
    SUCCESS,
    NAME_EMPTY,
    EMAIL_INVALID
}

// Functional interface for a validator
interface Validator extends Function<User, ValidationResult> {

    // Combinator: combines two validators
    default Validator and(Validator other) {
        return user -> {
            ValidationResult result = this.apply(user);
            return result == ValidationResult.SUCCESS ? other.apply(user) : result;
        };
    }
}

// Main class with validation logic
public class CombinatorExample {

    // Static validators
    static Validator nameNotEmpty = user ->
            (user.name == null || user.name.isEmpty()) ? ValidationResult.NAME_EMPTY : ValidationResult.SUCCESS;

    static Validator emailContainsAt = user ->
            (user.email != null && user.email.contains("@")) ? ValidationResult.SUCCESS : ValidationResult.EMAIL_INVALID;

    public static void main(String[] args) {
        // Combine validators using the combinator pattern
        Validator isValidUser = nameNotEmpty.and(emailContainsAt);

        User user = new User("Alice", "alice@example.com");
        System.out.println("Validation result: " + isValidUser.apply(user));  // SUCCESS

        User invalidUser = new User("", "aliceexample.com");
        System.out.println("Validation result: " + isValidUser.apply(invalidUser));  // NAME_EMPTY
    }
}

```

# Why use reactive programming?

Reactive programming is used to handle asynchronous, non-blocking operations efficiently, allowing systems to scale and respond faster under high load.

# Example of load testing on reactive vs imperative code

```java
@RestController
public class ReactiveController {

    private final List<String> users = List.of("Alice", "Bob", "Charlie");

    @GetMapping("/users-reactive")
    public Flux<String> getUsers() {
        // Simulate a delay (e.g., simulating a network call or DB access)
        return Flux.fromIterable(users)
                .delayElements(Duration.ofMillis(100)); // Delay each element by 100ms
    }
}
```

```java
@RestController
public class ImperativeController {

    @GetMapping("/users-imperative")
    public List<String> getUsers() throws InterruptedException {
        // Simulate some processing or latency
        Thread.sleep(100); // Optional: simulate delay for testing
        return List.of("Alice", "Bob", "Charlie");
    }
}
```

After running the service, I used a program called 'hey' to perform local load testing on the APIs.

It can be seen that because of the non-blocking behavior, the reactive controller performs better.

```bash
PS C:\WINDOWS\system32> hey -n 1000 -c 100 http://localhost:8080/users-reactive

Summary:
  Total:        3.3376 secs
  Slowest:      0.3440 secs
  Fastest:      0.3292 secs
  Average:      0.3337 secs
  Requests/sec: 299.6186


Response time histogram:
  0.329 [1]     |
  0.331 [42]    |■■■■
  0.332 [266]   |■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.334 [376]   |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.335 [187]   |■■■■■■■■■■■■■■■■■■■■
  0.337 [28]    |■■■
  0.338 [0]     |
  0.340 [0]     |
  0.341 [13]    |■
  0.343 [38]    |■■■■
  0.344 [49]    |■■■■■


Latency distribution:
  10% in 0.3312 secs
  25% in 0.3319 secs
  50% in 0.3328 secs
  75% in 0.3341 secs
  90% in 0.3406 secs
  95% in 0.3425 secs
  99% in 0.3436 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0007 secs, 0.3292 secs, 0.3440 secs
  DNS-lookup:   0.0004 secs, 0.0000 secs, 0.0072 secs
  req write:    0.0001 secs, 0.0000 secs, 0.0037 secs
  resp wait:    0.1099 secs, 0.1062 secs, 0.1151 secs
  resp read:    0.2230 secs, 0.2194 secs, 0.2265 secs

Status code distribution:
  [200] 1000 responses



PS C:\WINDOWS\system32> hey -n 1000 -c 100 http://localhost:8080/users-imperative

Summary:
  Total:        10.1376 secs
  Slowest:      3.5698 secs
  Fastest:      0.1091 secs
  Average:      0.8295 secs
  Requests/sec: 98.6422

  Total data:   25000 bytes
  Size/request: 25 bytes

Response time histogram:
  0.109 [1]     |
  0.455 [145]   |■■■■■■■■■■
  0.801 [237]   |■■■■■■■■■■■■■■■■
  1.147 [577]   |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  1.493 [4]     |
  1.839 [12]    |■
  2.186 [4]     |
  2.532 [8]     |■
  2.878 [8]     |■
  3.224 [0]     |
  3.570 [4]     |


Latency distribution:
  10% in 0.4440 secs
  25% in 0.6670 secs
  50% in 0.8907 secs
  75% in 0.8937 secs
  90% in 1.0036 secs
  95% in 1.0112 secs
  99% in 2.5675 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0006 secs, 0.1091 secs, 3.5698 secs
  DNS-lookup:   0.0004 secs, 0.0000 secs, 0.0055 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0007 secs
  resp wait:    0.8288 secs, 0.1090 secs, 3.5622 secs
  resp read:    0.0000 secs, 0.0000 secs, 0.0008 secs

Status code distribution:
  [200] 1000 responses



```

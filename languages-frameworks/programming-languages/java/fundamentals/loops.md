# Loops

## for

```java
for (int i = 0; i < 5; i++) {
    System.out.println("Iteration " + i);
}
```

## for each

```java
List<Integer> integerList = new ArrayList<>();
integerList.add(1);
integerList.add(2);
integerList.add(3);

for (Integer integer : integerList) {
    System.out.println(integer);
}
```

## while

```java
int count = 0;
while (count < 3) {
    System.out.println("Count: " + count);
    count++;
}
```

## do-while

```java
int num = 5;
do {
    System.out.println("Number is " + num);
    num--;
} while (num > 0);
```

same as while loop but guarantees at least one execution of the block of code.

## break

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        break; // Exit the loop when i equals 3
    }
    System.out.println("Iteration " + i);
}
```

## continue

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue; // Skip iteration when i equals 3
    }
    System.out.println("Iteration " + i);
}
```

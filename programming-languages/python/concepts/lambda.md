# Using lambda

```py
# Without lambda
numbers = [1,2,3,4,5,6,7,8,9]
def isEven(number):
  return number%2==0
evenNumbers = list(filter(isEven,numbers))
print(evenNumbers) #[2, 4, 6, 8]

```

```py
# With lambda
numbers = [1,2,3,4,5,6,7,8,9]
evenNumbers = list(filter(lambda x: x%2==0,numbers))
print(evenNumbers) #[2, 4, 6, 8]
```

We use lambda for inline definitions of small, anonymous functions without the need for a formal function definition. It is a **synthetic sugar** which makes code shorter.

# Recursion

- Recursion is a way to solve a problem by having a function call itself
- Any recursive method must have a terminating condition

[Recurrence Relation](Recurrence%20Relation%202ef680ebf65a473dbfd5ae3255e346de.md)

To solve recursively , 

- 
    1. What ‘s the simplest possible input ?
        
        ![Untitled](Untitled%2023.png)
        
    2. Play around with examples 
        
        ![Untitled](Untitled%2024.png)
        
    3. Relate hard cases to simpler cases
        
        ![Untitled](Untitled%2025.png)
        
        sum(4) = sum(3）+ 4
        
    4. Generalise the pattern
        
        ![Untitled](Untitled%2026.png)
        
    5. Write code by combining recursive pattern with base case 
        
        ![Untitled](Untitled%2027.png)
        
    

---

# eg. Factorial

n! = n*(n-1)*(n-2)*(n-3)...3*2*1

4! = 4*3*2*1

```python
def fact(n):
    if n>=1:
        return n*fact(n-1)
    else:
        return 1

print(fact(3))
```

![Untitled](Untitled%2028.png)

What ‘s the simplest possible input ?

sum(0) → 0 base case

---

# eg .Fibonacci sequence

> Fibonacci sequence 
1 , 1 , 2 , 3 , 5 , 8 , 13 , 21 , 34 ...
> 

Basically the nth number is the addition of its previous 2 numbers

```python
def fib(n):
    if n == 1 or n==2:
        return 1

    else:
        return fib(n-1)+fib(n-2)

```

---

# Tail Recursion

> Recursive call is last statement
> 

No need to keep previous function in the call stack
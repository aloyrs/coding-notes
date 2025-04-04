# Dynamic Programming

> Solves a problem by dividing into smaller sub-problems

Stores solution of sub-problems to avoid solving more than one once

Dynamic programming is a technique used to  optimise a recursive solution that does repeated work by storing solution of sub-problems , avoiding to solve them more than once
> 

*Keep thinking of not doing repeated work*

# When to use?

## Optimal substructure

- What is it?
    
    A problem has a optimal substructure if :
    
    The optimal solution of problem can be calculated from optimal sub-problems
    

## Overlapping sub-problems

- What is it?
    
    A problem has a overlapping sub-problems if :
    
    During the recursive process of dividing into subproblems , solve the same sub-problems more than once
    

[What is dynamic programming? - Inside code](https://www.youtube.com/watch?v=tOYZcy2IzJA)

```python
# Brute Force Recursion
def bruteForce(n):
    if n <= 1:
        return n
    return bruteForce(n - 1) + bruteForce(n - 2)
```

---

# Dynamic Programming Approaches

## Top-down ( Memoization )

- What is it ?
    
    > Solve problems using by storing the results of recursively called functions
    > 
    - Why is it called the top down approach?
        
        ![Untitled](Untitled%204.png)
        
        Starts by trying to solve the initial problem if not solve sub-problems
        

```python
# Memoization by using hashmap as cache to solve fibonnacci
def memoization(n, cache):
    if n <= 1:
        return n
    if n in cache:
        return cache[n]

    cache[n] = memoization(n - 1) + memoization(n - 2)
    return cache[n]
```

---

## Bottom-up ( Tabulation)

- What is it ?
    
    > Solve problems using by storing solutions of smaller subproblems to use to solve the main problem iteratively.
    > 
    
    ![Untitled](Untitled%205.png)
    

```python
# Tabulation
def dp(n):
    if n < 2:
        return n

    dp = [0, 1]
    i = 2
    while i <= n:
        tmp = dp[1]
        dp[1] = dp[0] + dp[1]
        dp[0] = tmp
        i += 1
    return dp[1]
```

---

# Multidimensional DP

1D DP - 1 variable

2D DP - 2 variable

[Introduction to Multi-dimensional Dynamic Programming](https://itnext.io/introduction-to-multi-dimensional-dynamic-programming-666b095b2e7b)
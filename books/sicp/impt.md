# Recursion thought process

base case + greedy solution

```py
def add(a,b):
  if a>b:
    return 0
  return a + add(a+1,b)

"""
add(2,5)
= 2 + add(3,5)
= a + add(a+1,b)
"""

```

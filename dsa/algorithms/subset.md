# Subset

> Non Adjacent combinations
> 

Number of subsets = $2^n$

**NO** duplicates from ordering

eg. Set = [1,2,3] 

One subset is [1,2]

But [2,1] is not a subset if not there is a duplicate 

if not it will be a [Permutation](Permutation%209abf6b45f617493c8312a7b2eb315256.md)

![Untitled](Untitled%2032.png)

# Subset visualisation

![3 elements : $2^n$ subsets = 8 ](Untitled%2033.png)

3 elements : $2^n$ subsets = 8 

At every branch , include 1 or [ ] meaning include 1 or not ...

At the bottom shows all 8 subsets of [1,2,3]

---

# How to solve subset questions?

*Think about the idea of taking or ignoring in the recursion call to build suitable subsets*

## Recursive

![Untitled](Untitled%2034.png)

## Iteratively

![Untitled](Untitled%2035.png)
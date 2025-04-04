# Greedy Algorithm

> Approach to solve a problem by selecting the best option currently available 

Selects the locally optimal choice at each step , hoping to acheive a global optimum
> 

- Simple , easy to implement , fast
- Usually don’t provide globally optimum solution
- Never reconsiders its choices

# Example

Find the maximum sum from root to node

![Actual=27, Greedy=21 , Greedy lost as it picked 7 first 
( locally optimum but not globally optimum)](Untitled%202.png)

Actual=27, Greedy=21 , Greedy lost as it picked 7 first 
( locally optimum but not globally optimum)

---

# When to use?

2 conditions :

## Greedy Choice Property

> Choosing the best option at each step can lead to a global optimal solution
> 

## Optimal substructure

> An optimal solution to the whole problem contains optimal solution to sub-problems
> 

---
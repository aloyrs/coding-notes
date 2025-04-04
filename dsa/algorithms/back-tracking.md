# Back Tracking

Back tracking is a method to solve problems by making a series of choices that we can back track to

- A brute force approach
- Used when there are multiple solutions and you want all those solutions

> How to know it is a back tracking problem?
When it says stuff like “Generate all” “Compute all”
> 

- Good example from reddit
    
    [Imagine you're in a maze.](http://i.solidfiles.net/845819db23.png) You don't know the way out, so you do the classical "only turn right" thing. [You go forward and turn right a few times, until you hit a dead end.](http://i.solidfiles.net/571b3e2176.png)
    
    Now, since you know that a dead end can't lead to the exit, you'll [retrace your steps back to the last intersection](http://i.solidfiles.net/35ac8dd827.png). When you get there, you [try out the next possible path to take](http://i.solidfiles.net/6a74dd38f8.png). Unfortunately, that one too leads to a dead end, so [you retrace your steps to the last intersection once again](http://i.solidfiles.net/fe130139de.png).
    
    Now, you notice that there are no additional paths to try to take from this intersection, because you have tried all the paths, and all the paths leads to dead ends. You now know that the exit can't be beyond this intersection, so what do you do? [You retrace your steps to the last intersection before the one you're at.](http://i.solidfiles.net/a71eccfc98.png)
    
    From this intersection, [you try the next available path](http://i.solidfiles.net/44038ec43a.png) (the first one to the right of the ones you haven't yet tried.) And voilà! The end!
    
    What you performed there was a backtracking algorithm. You exhausted the possible paths by trying them out one by one, and ticking off the ones that didn't work and retraced your steps. "Retracing your steps" in computer lingo is "backtracking."
    
    As you probably noticed, we were lucky to choose to start with always turning to the right. [Turning to the left wouldn't have been nearly as efficient.](http://i.solidfiles.net/aff493bcc7.png) Unfortunately, regardless of what method you use to choose your paths, there will always come mazes in which your method is not very efficient. This is because backtracking is a *brute force* algorithm. In the worst case, you'll have to try *all* the possible paths before succeeding.
    
    You don't need to learn trees and stacks or any other kind of data structures to familiarise yourself with backtacking algorithms. You could just represent a maze in a 2D array. Then you can print it out each step your program takes to try to solve the maze. (And as a bonus, I can reveal that backtracking algorithms are also really, really good at *creating* random mazes.)
    

---

# State Space Tree

![Example of ppossible seating arrangements for 2 boys and 1 girl](Untitled%203.png)

Example of ppossible seating arrangements for 2 boys and 1 girl

Can use a state space tree to represent the possible list of solutions for a given backtracking problem

---

3 keys by “Back to Back SWE” Youtube

1. Choice
    1. What choice to make at each call of function?
2. Constraints
    1. When to stop following a certain path?
3. Goal
    1. What are we trying to find? What is the target ?
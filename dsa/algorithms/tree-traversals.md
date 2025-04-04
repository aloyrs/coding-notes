# Tree Traversals

> Process of visiting each node in a tree exactly once
> 

![Untitled](Untitled%2042.png)

---

# Breadth First

### Pre-order Traversal

1. Print node
2. Traverse left 
3. Traverse right 

![Untitled](Untitled%2043.png)

Use “Data , Left , Right” to mark the nodes to see which path to go

### In order Traversal

1. Traverse left
2. Print node
3. Traverse right 
    
    ![output is in order 1 to 19](Untitled%2044.png)
    
    output is in order 1 to 19
    

![Untitled](Untitled%2045.png)

Use “ Left , Data , Right” to mark the nodes to see which path to go

### Post-order Traversal

1. Traverse left
2. Traverse right 
3. Print node
    
    ![Untitled](Untitled%2046.png)
    
    ![Untitled](Untitled%2047.png)
    

Use “ Left , Right , Data ” to mark the nodes to see which path to go

---

# Depth First

### Level order traversal

![Untitled](Untitled%2048.png)

Traverse level by level

![Untitled](Untitled%2049.png)

Uses a FIFO Queue

---
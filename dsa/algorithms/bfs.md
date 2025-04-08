# Breadth First Search (BFS)

Graph traversal method

Uses **QUEUE**

---

**TIME COMPLEXITY - O(N)**

---

**SPACE COMPLEXITY - O(B^D) / O(W)**

B is branching factor (max child per node eg. 2), D is depth (max distance from root)

W is width of biggest level

> _Max space needed in queue_

---

**HORIZONTAL then VERTICAL**

![dfs vs bfs.gif](dfs_vs_bfs.gif)

# How?

> Starts at some node , explore neighbour nodes , before moving on to next level neighbours
> ( Explores nodes in layers )

![Untitled](Untitled%2036.png)

Use FIFO queue to see which nodes is visited first

- Application : finding shortest path on unweighted graph

[Breadth First Search Implementation in Python](https://www.youtube.com/watch?v=U5-bRX2AHNY)

Python code implementation with explanation

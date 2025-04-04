# Depth First Search (DFS)

Graph traversal method

Uses **STACK**

**VERTICAL then HORIZONTAL**

![dfs vs bfs.gif](dfs_vs_bfs.gif)

# How?

> In a DFS, we always explore the deepest node; that is, we go one path as deep as possible, and if we hit the dead end, we back up and try a different path until we reach the end.
> 

![Untitled](Untitled%2037.png)

- Uses a stack to remember where it should go
- Application :
    - Cycle detection : 
    Encounter new edge that points to already visited vertex = cycle
    - Finding connected components
    - Topological sort
    - Maze Generation
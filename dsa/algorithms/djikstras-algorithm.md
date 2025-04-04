# Dijkstra’s Algorithm

> Algorithm for finding the shortest paths from a node to every other node
> 

[How Dijkstra's Algorithm Works](https://www.youtube.com/watch?v=EFg3u_E6eHU)

[Dijkstras Shortest Path Algorithm Explained | With Example | Graph Theory](https://www.youtube.com/watch?v=bZkzH5x0SKU)

![Untitled](Untitled%2040.png)

Set initial node as 0 and rest as **∞** tentatively

Repeat until all nodes explored

1. Update estimates
2. Choose next vertex
    1. Choose the vertex with smallest edge

***Do not update path lengths of already visited vertices**

# Example

![Untitled](Untitled%2041.png)

1. Explore node A : 
    1. path to C → 2
    2. path to F → 3
2. Choose F to explore next as its has the smallest edge (arrow) of 2

---

1. Explore node F : 
    1. path to C →  ~~4~~  but it is >3 so ignore , we want shortest
    2. path to E → 5
    3. path to B → 8
    4. path to G → 7
2. Choose C to explore next as its has the smallest edge (arrow) of 2

---

1. Explore node C : 
    1. path to D → 7
    2. path to E → 4 (<5 previously , improvement ! we take it)
2. Choose E to explore next as its has the smallest edge (arrow) of 1

... so on until all nodes are explored and we find the minimum distance to each node
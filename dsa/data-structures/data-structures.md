# Data Structures I actually need

# Abstract Data Type (ADT)

![Untitled](Untitled.png)

## Priority Queue

- Similar to a queue but each element has a priority
- An element with high priority is dequeued (lowest number = highest priority)

eg . Implement priority queue using a binary heap 
( because heaps have best possible time complexity)

---

# Arrays

*In Python, list is implemented as dynamic array, in other languages like Java, C++ there are both dynamic and static arrays

![Untitled](Untitled%201.png)

## Static Array

> Fixed length container which indexable n elements from [0,n-1]
> 

## Dynamic Array

> An array with automatic resizing
> 

|  | Static Array | Dynamic Array |  |
| --- | --- | --- | --- |
| Access | O(1) | O(1) | Access by index |
| Search | O(n) | O(n) | Traverse through array |
| Insertion | NA | O(n) | Have to shift all elements to right after insertion |
| Appending | NA | O(1) | Add to end  |
| Deletion | NA | O(n) | Have to shift elements after deletion  |

---

# Linked lists

Sequential list of vertices that hold data and point to other vertices that also hold data

## Terminology

| Head  | First node  |
| --- | --- |
| Tail | Last node |
| Pointer | reference to another node |
| Node | Object containing data and pointer |

![Untitled](Untitled%202.png)

## Singly Linked List

Only hold a reference to the next node

### Inserting into Singly

- Example
    
    ![Untitled](Untitled%203.png)
    
    ![Untitled](Untitled%204.png)
    
    ![Untitled](Untitled%205.png)
    

### Removing from Singly

- Example
    
    ![Untitled](Untitled%206.png)
    
    ![Untitled](Untitled%207.png)
    
    ![Untitled](Untitled%208.png)
    
    ![Untitled](Untitled%209.png)
    

## Doubly Linked List

Hold a reference to the next and previous

### Inserting into Doubly

- Example
    
    ![Untitled](Untitled%2010.png)
    
    ![Untitled](Untitled%2011.png)
    

### Removing from Doubly

- Example
    
    ![Untitled](Untitled%2012.png)
    
    ![4’s pointer to 15](Untitled%2013.png)
    
    4’s pointer to 15
    
    ![15’s previous pointer to 4](Untitled%2014.png)
    
    15’s previous pointer to 4
    
    ![Untitled](Untitled%2015.png)
    

|  | Pros | Cons |
| --- | --- | --- |
| Singly | Use less memory (pointers use memory)

Simpler Implementation | Cannot easily access previous elements
(Traverse from head to previous node)
 |
| Doubly | Can be traversed backwards | Takes 2x memory |

---

# Stack

Stores items in a **Last-In/First-Out (LIFO) or First-In/Last-Out (FILO) manner**

One-ended linear data structure with two primary operations : push & pop

![Untitled](Untitled%2016.png)

## Implementation

- list
- Linked list
- Collections.deque ✅
- queue.LifoQueue

---

# Queue

Stores items in a **First-In/First-Out (FIFO) manner**

Linear data structure which models a queue with two primary operations: enqueue & dequeue

![Untitled](Untitled%2017.png)

## Implementation

- list ❌
- collections.deque ✅
- queue.Queue
- multiprocessing.Queue

---

# Tree

- Undirected graph
- Acyclic (No cycles)
- N nodes with N-1 edges
- Only 1 path between nodes

## Terminology

Leaf node - nodes with no children

Subtree 

![Subtree - Tree entirely contained within another](Untitled%2018.png)

Subtree - Tree entirely contained within another

## Binary Tree

Tree with every node at least 2 children

## Binary Search Tree

Binary Tree that satisfies the BST invariant 

BST invariant

> left subtree : smaller elements
right subtree : larger elements
> 

![Worst comes from a chain of increasing elements](Untitled%2019.png)

Worst comes from a chain of increasing elements

### Insertion

![Average : O(logn)](Untitled%2020.png)

Average : O(logn)

![O(n)](Untitled%2021.png)

O(n)

### Removing

Find
Scenarios: 
- hit null node , not found
- comparator value = 0 , found
- comparator < 0 , is in left subtree
- comparator > 0 , is in right subtree

Replace node with successor to maintain BST invariant 

Case 1 : Leaf node

- Remove without any side effect

Case 2 & 3 : Either left/right child node is a subtree

![Untitled](Untitled%2022.png)

![Untitled](Untitled%2023.png)

![Untitled](Untitled%2024.png)

Remove 9 the child 7 replaces it 

Case 4 : Node has both left & right subtree

> Which subtree will be the successor of the node to be removed ??????
Either :
- Largest in left subtree 
OR
- Smallest in right subtree
> 

![Untitled](Untitled%2025.png)

![Using smallest in right subtree , dig left all the way from 20 to find 11](Untitled%2026.png)

Using smallest in right subtree , dig left all the way from 20 to find 11

![Switch 11 with 7 , remove old 11 ](Untitled%2027.png)

Switch 11 with 7 , remove old 11 

## Traversal

![Untitled](Untitled%2028.png)

### Pre-order Traversal

1. Print node
2. Traverse left 
3. Traverse right 

![Untitled](Untitled%2029.png)

![Rebalance tree ](Untitled%2030.png)

Rebalance tree 

### In order Traversal

1. Traverse left
2. Print node
3. Traverse right 
    
    ![output is in order 1 to 19](Untitled%2031.png)
    
    output is in order 1 to 19
    

### Post-order Traversal

1. Traverse left
2. Traverse right 
3. Print node
    
    ![Untitled](Untitled%2032.png)
    

### Level order traversal

![Untitled](Untitled%2033.png)

---

# Heap

USE BINARY HEAP TO IMPLEMENT PRIORITY QUEUE

Tree based data structure that satisfies the heap invariant (aka. heap property)

> **Heap invariant :** 
Value of parent vertex is always ≥ value of all child vertex (max heap)
Value of parent vertex is always ≤ value of all child vertex (min heap)
> 

![Untitled](Untitled%2034.png)

![Untitled](Untitled%2035.png)

## Binary Heap

- Each parent node has 2 children

### Inserting

Swap with parent node if doesn’t follow heap invariant

### Removing

Remove Root

Using **poll()**

![Swap last element with root element](Untitled%2036.png)

Swap last element with root element

![Untitled](Untitled%2037.png)

![Swap 10 with 1 as does not follow heap invariant 
( “Bubble down”)](Untitled%2038.png)

Swap 10 with 1 as does not follow heap invariant 
( “Bubble down”)

![Untitled](Untitled%2039.png)

Remove element not root 

![Remove 12 , swap with last element 3](Untitled%2040.png)

Remove 12 , swap with last element 3

![Untitled](Untitled%2041.png)

![Bubble up for heap invariant](Untitled%2042.png)

Bubble up for heap invariant

Removing binary heap element using hash table 
→ time complexity O(1) as can find elements by look up at hash table 

![Untitled](Untitled%2043.png)

---

# Hash Table/Hash map

![Untitled](Untitled%2044.png)

A data structure provide mapping from key to value using hashing

## Hash function

**H(x)** is a function that maps key ‘x’ to whole number in a range 

![Untitled](Untitled%2045.png)

key → hash function converts key to an index → index to value

$H(x) = (x^2 + 3) mod10$

if key x = 3 , 

$H(3) = (3^2 + 3) mod10 = 2$

![Key 3 is at index 2](Untitled%2046.png)

Key 3 is at index 2

## Time complexity

![Untitled](Untitled%2047.png)

## Collision Handling in Hash Table

Happens when different keys are hashed to the same value 

### Seperate Chaining

Create a linked list at the index , append to the link list when collision occurs

![Untitled](Untitled%2048.png)

### Open Addressing

1. Linear Probing
2. Quadratic Probing 
3. Double hashing

Load Factor ( $α$ ) = items in table / size of table

![Chaining vs Linear Probing . Linear Probing exponentially bad as approaching 0.8 and above](Untitled%2049.png)

Chaining vs Linear Probing . Linear Probing exponentially bad as approaching 0.8 and above

![N is size of hashtable, P(k,x) is the probing function](Untitled%2050.png)

N is size of hashtable, P(k,x) is the probing function

### Linear Probing

![**a** and **N** should be relatively prime , have their Greatest Common Denominator (GCD) as 1 to avoid infinite loop](Untitled%2051.png)

**a** and **N** should be relatively prime , have their Greatest Common Denominator (GCD) as 1 to avoid infinite loop

To avoid infinite loop in Linear Probing , usually P(x) = x , where a =1

so while loop will increase the index by one every loop , 

find next available slot for the key

Linearly searching for the next empty slot to prevent collision

![Untitled](Untitled%2052.png)

### Quadratic Probing

 

![Untitled](Untitled%2053.png)

If index is taken , probe with P(0) then P(1) so on until an empty slot is found

![empty slot at 0 was found after probing with P(2)](Untitled%2054.png)

empty slot at 0 was found after probing with P(2)

### Double Hashing

Probes by using a second hash function with a constant multiplier 

index = hash1(k) + x*hash2(k)

![Untitled](Untitled%2055.png)

*constant multiplier(x)  : 0 → until empty index

P(0) → index = hash1(k) + 1*hash2(k)

P(1) → index = hash1(k) + 1*hash2(k)

...

### Removing in Open Addressing

Remove and replace with “🪦”( tombstone )

When searching with probing, skip over “🪦” and keep probing

---

# Graph

Non-linear data structure consisting of vertices and edges

Used to represent networks

Undirected Graph - no direction between vertices 

Directed Graph - one direction between vertices 

![Untitled](Untitled%2056.png)

Weighted Graph - Each edge has a value

---

# Trie

aka. prefix tree / digital tree

- Came from re**TRIE**val , trie is used for retrieving things
- Used for storing strings/characters
- Check if a string is in the set of strings

![Untitled](Untitled%2057.png)
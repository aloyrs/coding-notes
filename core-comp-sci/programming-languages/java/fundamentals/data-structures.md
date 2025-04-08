# Array

> Fixed sized list for storing elements of the same data type

```java
int[] sizeThreeArray = new int[3];
myArray[0] = 1;
myArray[1] = 2;
myArray[2] = 3;

int[] sizeThreeArrayWithElements = {1, 2, 3};
```

# ArrayList

> Dynamic sized array for storing elements of the same data type

```java
ArrayList<String> cars = new ArrayList<String>();
cars.add("Volvo");
cars.add("BMW");
cars.add("Ford");
cars.add("Mazda");

 // Access elements
int thirdCar = cars.get(2);

// Changing element from index 1
cars.set(1, "Toyota");

// Get size
int size = myList.size();

// Check contains element
boolean found = myList.contains("Mazda");

// Remove element
myList.remove("Ford");

// Sorting elements (alphabetically/numerically)
Collections.sort(myList);

// Iterating over elements using a for-each loop
for (int element : myList) {
    System.out.print(element + " ");
}

// Clearing the ArrayList
myList.clear();
```

# Linked List

> Consists of a sequence of nodes, where each node stores a data element and a reference (or link) to the next node in the sequence

| Component          | ?                                                                                                |
| ------------------ | ------------------------------------------------------------------------------------------------ |
| Node               | Contains data & pointer to next node                                                             |
| Head               | Reference to first node of the linked list                                                       |
| Tail               | Reference to last node of the linked list                                                        |
| Singly Linked List | Only allows traversal in one direction , head to tail                                            |
| Doubly Linked List | Allows bidirectional traversal, each node has references to both the next and the previous nodes |

Implement using java.util.LinkedList

```java
LinkedList<String> linkedList = new LinkedList<>();

// Add elements to the list
linkedList.add("First");
linkedList.add("Second");
linkedList.add("Third");

// Display the contents of the list
System.out.println("LinkedList: " + linkedList);

// Add an element at a specific index
linkedList.add(1, "NewElement");

// Remove an element by value
linkedList.remove("Second");

// Remove an element by index
linkedList.remove(2);

// Get the size of the list
int size = linkedList.size();

// Check if the list is empty
boolean isEmpty = linkedList.isEmpty();
```

# Stack

> Last In First Out (LIFO) Data Structure

Implement using an java.util.ArrayList :

```java
Stack<Integer> stack = new Stack<>();

stack.push(1);
stack.push(2);

System.out.println("Stack size: " + stack.size()); // Stack size: 2

int top = stack.pop();
System.out.println("Popped element: " + top); // Popped element: 2

int peeked = stack.peek();
System.out.println("Peeked element: " + peeked); // Peeked element: 1

System.out.println("Is stack empty? " + stack.isEmpty()); // Is stack empty? false
```

Implement using java.util.Stack

```java
Stack<Integer> stack = new Stack<>();

// Push elements onto the stack
stack.push(1);
stack.push(2);
stack.push(3);

// Peek at the top element without removing it
int peeked = stack.peek();
System.out.println("Peeked element: " + peeked); // Output: Peeked element: 3

// Pop an element from the stack
int popped = stack.pop();
System.out.println("Popped element: " + popped); // Output: Popped element: 3

// Check if the stack is empty
boolean isEmpty = stack.isEmpty();
System.out.println("Is stack empty? " + isEmpty); // Output: Is stack empty? false

// Get the size of the stack
int size = stack.size();
System.out.println("Stack size: " + size); // Output: Stack size: 2
```

# Queue

> First In First Out (FIFO) Data Structure

Implement using java.util.LinkedList:

```java
Queue<String> queue = new LinkedList<>();

// Enqueue
queue.offer("element");

// Dequeue
String element = queue.poll();

String frontElement = queue.peek();
```

Implement using java.util.ArrayDeque:

```java
Queue<String> queue = new ArrayDeque<>();

// Enqueue
queue.offer("element");

// Dequeue
String element = queue.poll();

String frontElement = queue.peek();
```

# Hash Map

> Store data in key:value pair format

```java
// Create a HashMap
Map<String, Integer> hashMap = new HashMap<>();

// Add key-value pairs to the HashMap
hashMap.put("Alice", 28);
hashMap.put("Bob", 35);
hashMap.put("Charlie", 22);

// Retrieve values from the HashMap
int aliceAge = hashMap.get("Alice");
int bobAge = hashMap.get("Bob");

// Check if a key exists in the HashMap
boolean containsKey = hashMap.containsKey("Alice");
boolean containsKey2 = hashMap.containsKey("David");

// Remove a key-value pair from the HashMap
hashMap.remove("Charlie");

// Check if the HashMap is empty
boolean isEmpty = hashMap.isEmpty();

// Get the size of the HashMap
int size = hashMap.size();
```

# Hash Set

> Store unique values in no particular order

```java
// Create a HashSet
Set<String> hashSet = new HashSet<>();

// Add elements to the HashSet
hashSet.add("Apple");
hashSet.add("Banana");
hashSet.add("Cherry");

// Check if an element exists in the HashSet
boolean containsApple = hashSet.contains("Apple");
boolean containsGrape = hashSet.contains("Grape");

// Remove an element from the HashSet
hashSet.remove("Cherry");

// Check if the HashSet is empty
boolean isEmpty = hashSet.isEmpty();

// Get the size of the HashSet
int size = hashSet.size();
```

# Binary Tree

> Hierarchical data structure consisting of nodes, where each node has at most two children: a left child and a right child

```java
class TreeNode {
    int data;
    TreeNode left;
    TreeNode right;

    public TreeNode(int data) {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Create the root node
TreeNode root = new TreeNode(10);

// Build the binary tree
root.left = new TreeNode(5);
root.right = new TreeNode(15);
root.left.left = new TreeNode(3);
root.left.right = new TreeNode(7);
root.right.left = new TreeNode(12);
root.right.right = new TreeNode(18);

// Can implement algorithms for binary tree such as traversals /search
```

# Heap

> A specialized tree-based data structure that satisfies the heap property

Heap property:

- min heap , root is min value
- max heap , root is max value

```java
// Create a min-heap using PriorityQueue
PriorityQueue<Integer> minHeap = new PriorityQueue<>();

// Insert elements into the min-heap
minHeap.offer(5);
minHeap.offer(10);
minHeap.offer(3);
minHeap.offer(7);

// Peek at the minimum element
int minElement = minHeap.peek();
System.out.println("Minimum element: " + minElement);

// Remove and display elements in ascending order (sorted)
while (!minHeap.isEmpty()) {
    int element = minHeap.poll();
    System.out.print(element + " ");
}
```

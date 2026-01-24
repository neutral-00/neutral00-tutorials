# Data Structure Classification (Java – DSA)

Data structures are ways of organizing and storing data so that it can be accessed and modified efficiently. In DSA, data structures are commonly classified based on **how data elements are arranged and related to each other**.

---

## Main Classification of Data Structures

Data structures can be broadly classified into:

1. **Linear Data Structures**
2. **Non-Linear Data Structures**
3. **Hash-Based Data Structures**

---

## 1️⃣ Linear Data Structures (Horizontal Tree)

```
LINEAR DATA STRUCTURES
|
+--> ARRAY
|
+--> LINKED LIST
|
+--> STACK  (LIFO)
|
+--> QUEUE  (FIFO)
```

---

## 2️⃣ Non-Linear Data Structures (Horizontal Tree)

```
NON-LINEAR DATA STRUCTURES
|
+--> TREE
|     |
|     +--> BINARY TREE
|           |
|           +--> BST
|           |
|           +--> HEAP
|
+--> GRAPH
```

---

## 3️⃣ Hash-Based Data Structures (Horizontal Tree)

```
HASH-BASED DATA STRUCTURES
|
+--> HASHMAP   (Key–Value)
|
+--> HASHSET   (Unique Keys)
```
## 1. Linear Data Structures

In linear data structures, elements are arranged sequentially, one after another. Each element (except the first and last) has a **single predecessor and a single successor**.

### Characteristics

- Data elements are stored in a linear order
- Easy to traverse
- Memory may or may not be contiguous

### Examples

#### a) Array

- Fixed size
- Contiguous memory allocation
- Fast access using index

```java
int[] arr = {1, 2, 3, 4};
```

**Time Complexity (Access):** O(1)

---

#### b) Linked List

- Dynamic size
- Non-contiguous memory allocation
- Each node stores data and reference(s) to the next or previous node

```java
class Node {
    int data;
    Node next;
}
```

---

#### c) Stack (LIFO – Last In First Out)
- A linear data structure which follow the Last In First Out prinicple.
- Meaning element that come last is the one that will be removed first.
Operations:

- push
- pop
- peek

```java
Stack<Integer> stack = new Stack<>();
stack.push(10);
stack.pop();
```

---

#### d) Queue (FIFO – First In First Out)

- A linear data structure which follow the First In First Out prinicple.
- Meaning element that come first is the one that will be removed first.
Operations:

- enqueue
- dequeue

```java
Queue<Integer> queue = new LinkedList<>();
queue.offer(10);
queue.poll();
```

---

## 2. Non-Linear Data Structures

In non-linear data structures, elements are **not arranged sequentially**. One element can be connected to multiple elements.

### Characteristics

- Hierarchical or graph-based structure
- More complex relationships
- Efficient for representing real-world problems

---

### Examples

#### a) Tree
It is a non-linear data structure that is Hierarchical in nature. \
It has a Root, and then parent and child relationships. \
Children at the last level of the hierarchy do not have child nodes and are known as leaf nodes.

**NOTE**
- There can not be cycles in the tree.

Common types:

- Binary Tree
- Binary Search Tree (BST)
- Heap

```java
class TreeNode {
    int data;
    TreeNode left, right;
}
```

---

#### b) Graph

- Collection of vertices (nodes) and edges
- Can be directed or undirected
- Can be connected or non-connected
- Can be cyclic or non-cyclic
- can be weighted or non-weighted

```java
class Graph {
    int vertices;
    List<Integer>[] adjList;
}
```

---

## 3. Hash-Based Data Structures

Hash-based data structures store data using a **key-value pair** and a **hash function** to map keys to indexes.

### Characteristics

- Fast insertion, deletion, and search
- No guaranteed ordering
- Uses hashing

---

### Examples

#### a) HashMap

```java
HashMap<Integer, String> map = new HashMap<>();
map.put(1, "Apple");
map.get(1);
```

Average Time Complexity:

- Insert: O(1)
- Search: O(1)

---

#### b) HashSet

```java
HashSet<Integer> set = new HashSet<>();
set.add(10);
set.contains(10);
```

---

## Summary Table

| Category   | Data Structures                  |
| ---------- | -------------------------------- |
| Linear     | Array, Linked List, Stack, Queue |
| Non-Linear | Tree, Graph                      |
| Hash-Based | HashMap, HashSet                 |

---

## Key Takeaways

- Linear structures store data sequentially
- Non-linear structures represent complex relationships
- Hash-based structures provide fast access using keys
- Choosing the right data structure improves performance

---


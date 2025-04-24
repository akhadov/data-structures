# C# Data Structures

## Introduction

Welcome to the C# Data Structures repository! This comprehensive guide explores the fundamental data structures implemented in C#, providing clear explanations, examples, and best practices for their use.

This repository divides data structures into the following categories:

### 1. Built-in Data Structures
#### 1.1 Array-Based Collections
- Arrays (Single and Multi-dimensional)
  - **Single-dimensional Arrays**
    - A contiguous block of memory storing elements of the same type
    - Zero-based indexing (accessing elements via `array[index]`)
    - Fixed size once initialized, cannot grow or shrink dynamically
    - Declaration: `type[] arrayName = new type[size];`
    - Time complexity: O(1) for random access, O(n) for insertion/deletion
    - Common operations: indexing, iterating, sorting, searching, filtering
    - Example:
      ```csharp
      int[] numbers = new int[5]; // Creates array of 5 integers
      numbers[0] = 10;            // Assigns value to first element
      int value = numbers[0];     // Retrieves first element
      ```
    
  - **Multi-dimensional Arrays**
    - **Rectangular Arrays** 
      - Each row has the same number of columns
      - Declaration: `type[,] arrayName = new type[rows, columns];`
      - Accessed via `array[row, column]`
      - Memory-efficient for matrix operations
      - Example:
        ```csharp
        int[,] matrix = new int[3, 4]; // 3 rows, 4 columns
        matrix[0, 0] = 1;              // First element
        int value = matrix[2, 3];      // Last element
        ```
    
    - **Jagged Arrays** 
      - Arrays of arrays, where each inner array can have different lengths
      - More flexible than rectangular arrays
      - Declaration: `type[][] arrayName = new type[outerSize][];`
      - Each inner array must be initialized separately
      - Accessed via `array[outerIndex][innerIndex]`
      - Example:
        ```csharp
        int[][] jaggedArray = new int[3][];
        jaggedArray[0] = new int[4];   // First row has 4 columns
        jaggedArray[1] = new int[2];   // Second row has 2 columns
        jaggedArray[2] = new int[5];   // Third row has 5 columns
        jaggedArray[0][0] = 1;         // Assigns value to first element
        ```

  - **Performance Considerations**
    - Arrays provide the fastest access time among collections
    - Memory is allocated contiguously, which improves cache locality
    - Fixed size can lead to inefficiency when the number of elements is unknown
    - For operations requiring frequent resizing, consider using `List<T>`
    - Row-major ordering in C# (elements in the same row are stored contiguously)

- Lists
  - List<T>
  - ArrayList (Legacy)
  - ReadOnlyCollection<T>

#### 1.2 Key-Value Collections
- Dictionaries
  - Dictionary<TKey, TValue>
  - SortedDictionary<TKey, TValue>
  - ConcurrentDictionary<TKey, TValue>
- HashSets
  - HashSet<T>
  - SortedSet<T>

#### 1.3 FIFO/LIFO Collections
- Queues
  - Queue<T>
  - ConcurrentQueue<T>
  - PriorityQueue<TElement, TPriority>
- Stacks
  - Stack<T>
  - ConcurrentStack<T>

### 2. Linear Data Structures
#### 2.1 Linked Lists
- Singly Linked Lists
  - Implementation
  - Operations
- Doubly Linked Lists
  - LinkedList<T>
  - Custom Implementation
- Circular Linked Lists
  - Singly Circular
  - Doubly Circular

#### 2.2 Advanced Linear Structures
- Skip Lists
  - Probabilistic Data Structure
  - Implementation
- Sparse Arrays
- XOR Linked Lists

### 3. Tree-based Data Structures
#### 3.1 Binary Trees
- Basic Binary Trees
- Binary Search Trees
  - Implementation
  - Traversal Methods (In-order, Pre-order, Post-order)
- Balanced Trees
  - AVL Trees
  - Red-Black Trees

#### 3.2 Multi-way Trees
- B-Trees
- B+ Trees
- 2-3 Trees
- 2-3-4 Trees

#### 3.3 Specialized Trees
- Tries (Prefix Trees)
- Radix Trees
- Suffix Trees
- Quad Trees
- Octrees

### 4. Graph Data Structures
#### 4.1 Graph Representations
- Adjacency Matrix
- Adjacency List
- Incidence Matrix

#### 4.2 Graph Types
- Directed Graphs (Digraphs)
- Undirected Graphs
- Weighted Graphs
- Directed Acyclic Graphs (DAGs)

#### 4.3 Graph Operations
- Graph Traversal (BFS, DFS)
- Minimum Spanning Trees
- Shortest Path Algorithms

### 5. Advanced Data Structures
#### 5.1 Heaps and Priority Structures
- Priority Queues
- Binary Heaps
  - Min Heap
  - Max Heap
- Fibonacci Heaps

#### 5.2 Probabilistic Data Structures
- Bloom Filters
- Count-Min Sketch
- HyperLogLog

#### 5.3 Specialized Data Structures
- Disjoint Set (Union-Find)
- Segment Trees
- Fenwick Trees (Binary Indexed Trees)
- Sparse Tables
- Interval Trees

## Getting Started

Navigate to each folder to explore specific data structures, or follow the structured learning path outlined in the documentation.

# C# Data Structures

<style>
/* Improved styling for collapsible sections */
details {
  padding: 0.5em 0.5em 0;
  border-radius: 4px;
  overflow: hidden;
  background-color: #f8f9fa;
  margin-bottom: 0.5em;
}

details summary {
  padding: 0.5em;
  border-radius: 4px;
  cursor: pointer;
  margin: -0.5em -0.5em 0;
  background-color: #e9ecef;
}

details summary:hover {
  background-color: #dee2e6;
}

/* Progressive indentation with subtle visual cues */
details details {
  margin-left: 25px;
  border-left: 2px solid #6c757d;
  padding-left: 10px;
  background-color: #ffffff;
}

details details details {
  margin-left: 25px;
  border-left: 2px solid #5a6268;
}

details details details details {
  margin-left: 25px;
  border-left: 2px solid #495057;
}

/* Code block styling */
code {
  background-color: #f1f3f5;
  padding: 2px 4px;
  border-radius: 3px;
  font-family: monospace;
}

pre code {
  display: block;
  padding: 10px;
  overflow-x: auto;
  line-height: 1.4;
  border-radius: 4px;
  border: 1px solid #dee2e6;
}
</style>

## Introduction

Welcome to the C# Data Structures repository! This comprehensive guide explores the fundamental data structures implemented in C#, providing clear explanations, examples, and best practices for their use.

This repository divides data structures into the following categories:

<details>
<summary><strong>1. Built-in Data Structures</strong></summary>

<details>
<summary><strong>1.1 Array-Based Collections</strong></summary>

<details>
<summary><strong>Arrays (Single and Multi-dimensional)</strong></summary>

#### Single-dimensional Arrays
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

#### Multi-dimensional Arrays
<details>
<summary><strong>Rectangular Arrays</strong></summary>

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
</details>

<details>
<summary><strong>Jagged Arrays</strong></summary>

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
</details>

#### Performance Considerations
- Arrays provide the fastest access time among collections
- Memory is allocated contiguously, which improves cache locality
- Fixed size can lead to inefficiency when the number of elements is unknown
- For operations requiring frequent resizing, consider using `List<T>`
- Row-major ordering in C# (elements in the same row are stored contiguously)
</details>

<details>
<summary><strong>Lists</strong></summary>

#### List&lt;T&gt;
- Dynamic array implementation that can resize itself as needed
- Provides methods to search, sort, and manipulate lists
- Time complexity: O(1) for access, O(n) for insertion/deletion, O(n) for resizing
- Example:
  ```csharp
  List<string> names = new List<string>();
  names.Add("Alice");            // Adds element to the end
  names.Insert(0, "Bob");        // Inserts at specific position
  string first = names[0];       // Access by index
  names.Remove("Alice");         // Removes specific element
  ```

#### ArrayList (Legacy)
- Non-generic collection that can store objects of any type
- Less type-safe and requires boxing/unboxing for value types
- Replaced by List&lt;T&gt; in modern C# code
- Example:
  ```csharp
  ArrayList list = new ArrayList();
  list.Add(10);                  // Adds an int (boxed)
  list.Add("Hello");             // Adds a string
  int num = (int)list[0];        // Requires explicit cast
  ```

#### ReadOnlyCollection&lt;T&gt;
- Provides a read-only wrapper around a collection
- Prevents modification of the collection through this wrapper
- Useful for returning collections from methods/properties that shouldn't be modified
- Example:
  ```csharp
  List<int> numbers = new List<int> { 1, 2, 3 };
  ReadOnlyCollection<int> readOnly = new ReadOnlyCollection<int>(numbers);
  // readOnly[0] = 10;           // This would cause a compile error
  // Changes to the original list are still visible through the wrapper
  numbers.Add(4);                // readOnly will now contain 4 as well
  ```
</details>
</details>

<details>
<summary><strong>1.2 Key-Value Collections</strong></summary>

<details>
<summary><strong>Dictionaries</strong></summary>

#### Dictionary&lt;TKey, TValue&gt;
- Collection of key-value pairs with O(1) average lookup time
- Uses hash table implementation
- Keys must be unique and cannot be null
- Example:
  ```csharp
  Dictionary<string, int> scores = new Dictionary<string, int>();
  scores["Alice"] = 95;          // Add or update a key-value pair
  int aliceScore = scores["Alice"]; // Retrieve value by key
  bool exists = scores.ContainsKey("Bob"); // Check if key exists
  ```

#### SortedDictionary&lt;TKey, TValue&gt;
- Dictionary that keeps keys in sorted order
- Uses a balanced binary tree (red-black tree)
- Slightly slower than Dictionary for access (O(log n))
- Example:
  ```csharp
  SortedDictionary<string, int> sorted = new SortedDictionary<string, int>();
  sorted["Charlie"] = 80;
  sorted["Alice"] = 95;
  sorted["Bob"] = 85;
  // Keys will be enumerated in order: Alice, Bob, Charlie
  ```

#### ConcurrentDictionary&lt;TKey, TValue&gt;
- Thread-safe version of Dictionary
- Supports concurrent updates from multiple threads
- Higher overhead than Dictionary
- Example:
  ```csharp
  ConcurrentDictionary<string, int> concurrent = new ConcurrentDictionary<string, int>();
  concurrent.TryAdd("Alice", 95);
  concurrent.AddOrUpdate("Bob", 85, (key, oldValue) => oldValue + 10);
  ```
</details>

<details>
<summary><strong>HashSets</strong></summary>

#### HashSet&lt;T&gt;
- Collection of unique elements with no specific order
- Fast lookup, addition, and removal (O(1) average)
- Useful for eliminating duplicates and set operations
- Example:
  ```csharp
  HashSet<int> numbers = new HashSet<int> { 1, 2, 3 };
  numbers.Add(2);                // No effect (duplicate)
  numbers.Add(4);                // Adds new element
  bool contains = numbers.Contains(3); // Fast lookup
  // Set operations
  HashSet<int> other = new HashSet<int> { 3, 4, 5 };
  numbers.UnionWith(other);      // Union
  numbers.IntersectWith(other);  // Intersection
  ```

#### SortedSet&lt;T&gt;
- Set that maintains elements in sorted order
- O(log n) for most operations
- Based on red-black tree
- Example:
  ```csharp
  SortedSet<string> names = new SortedSet<string> { "Charlie", "Alice", "Bob" };
  names.Add("David");
  // Elements are enumerated in order: Alice, Bob, Charlie, David
  string first = names.Min;      // Gets the smallest element
  string last = names.Max;       // Gets the largest element
  ```
</details>
</details>

<details>
<summary><strong>1.3 FIFO/LIFO Collections</strong></summary>

<details>
<summary><strong>Queues</strong></summary>

#### Queue&lt;T&gt;
- First-in, first-out (FIFO) collection
- Elements are added to the end and removed from the beginning
- Common operations: Enqueue, Dequeue, Peek
- Example:
  ```csharp
  Queue<string> queue = new Queue<string>();
  queue.Enqueue("First");        // Add to the end
  queue.Enqueue("Second");
  string first = queue.Peek();   // View first item without removing
  string removed = queue.Dequeue(); // Remove and return first item
  ```

#### ConcurrentQueue&lt;T&gt;
- Thread-safe queue implementation
- Safe for multiple threads to enqueue and dequeue simultaneously
- Example:
  ```csharp
  ConcurrentQueue<int> concurrentQueue = new ConcurrentQueue<int>();
  concurrentQueue.Enqueue(1);
  concurrentQueue.Enqueue(2);
  bool success = concurrentQueue.TryDequeue(out int result);
  ```

#### PriorityQueue&lt;TElement, TPriority&gt;
- Queue where elements are dequeued according to priority rather than insertion order
- Added in .NET 6
- Example:
  ```csharp
  PriorityQueue<string, int> priorityQueue = new PriorityQueue<string, int>();
  priorityQueue.Enqueue("High", 1);    // Lower number = higher priority
  priorityQueue.Enqueue("Low", 3);
  priorityQueue.Enqueue("Medium", 2);
  string highest = priorityQueue.Dequeue(); // Returns "High"
  ```
</details>

<details>
<summary><strong>Stacks</strong></summary>

#### Stack&lt;T&gt;
- Last-in, first-out (LIFO) collection
- Elements are added and removed from the same end
- Common operations: Push, Pop, Peek
- Example:
  ```csharp
  Stack<int> stack = new Stack<int>();
  stack.Push(1);                 // Add to top
  stack.Push(2);
  int top = stack.Peek();        // View top item without removing
  int popped = stack.Pop();      // Remove and return top item
  ```

#### ConcurrentStack&lt;T&gt;
- Thread-safe stack implementation
- Safe for multiple threads to push and pop simultaneously
- Example:
  ```csharp
  ConcurrentStack<int> concurrentStack = new ConcurrentStack<int>();
  concurrentStack.Push(1);
  concurrentStack.Push(2);
  bool success = concurrentStack.TryPop(out int result);
  ```
</details>
</details>
</details>

<details>
<summary><strong>2. Linear Data Structures</strong></summary>

<details>
<summary><strong>2.1 Linked Lists</strong></summary>

<details>
<summary><strong>Singly Linked Lists</strong></summary>

#### Implementation
- Each node contains data and a reference to the next node
- Head points to the first node, last node points to null
- Efficient insertions and deletions at the beginning
- Example node class:
  ```csharp
  public class Node<T> {
      public T Data { get; set; }
      public Node<T> Next { get; set; }
      
      public Node(T data) {
          Data = data;
          Next = null;
      }
  }
  ```

#### Operations
- Insertion: O(1) at head, O(n) elsewhere
- Deletion: O(1) at head, O(n) elsewhere
- Access: O(n) for random access
- Search: O(n) in worst case
</details>

<details>
<summary><strong>Doubly Linked Lists</strong></summary>

#### LinkedList&lt;T&gt;
- Built-in C# implementation of doubly linked list
- Each node has references to both previous and next nodes
- Provides efficient insertion/deletion at any position
- Example:
  ```csharp
  LinkedList<string> list = new LinkedList<string>();
  list.AddLast("End");
  LinkedListNode<string> firstNode = list.AddFirst("Start");
  list.AddAfter(firstNode, "Middle");
  list.Remove("End");
  ```

#### Custom Implementation
- Example doubly linked list node:
  ```csharp
  public class DoublyNode<T> {
      public T Data { get; set; }
      public DoublyNode<T> Next { get; set; }
      public DoublyNode<T> Previous { get; set; }
      
      public DoublyNode(T data) {
          Data = data;
          Next = null;
          Previous = null;
      }
  }
  ```
- Advantages over singly linked: Bidirectional traversal, O(1) deletion given the node
</details>

<details>
<summary><strong>Circular Linked Lists</strong></summary>

#### Singly Circular
- Last node points back to the first node
- Efficient cycling through elements
- No null references
- Useful for round-robin scheduling

#### Doubly Circular
- Combination of doubly linked and circular
- Last node's next points to first, first node's previous points to last
- Allows traversal in either direction with no beginning or end
</details>
</details>

<details>
<summary><strong>2.2 Advanced Linear Structures</strong></summary>

<details>
<summary><strong>Skip Lists</strong></summary>

#### Probabilistic Data Structure
- Multi-level linked list with probabilistic balancing
- Average case: O(log n) for search, insert, delete
- Alternative to balanced trees with simpler implementation

#### Implementation
- Elements appear in multiple levels
- Higher levels act as express lanes
- Probability-based promotion to higher levels
</details>

<details>
<summary><strong>Sparse Arrays</strong></summary>

- Efficiently stores arrays with many default values
- Only allocates memory for non-default elements
- Uses hash map or linked lists internally
- Common in scientific and mathematical applications
</details>

<details>
<summary><strong>XOR Linked Lists</strong></summary>

- Memory-efficient linked list implementation
- Each node stores XOR of addresses of previous and next nodes
- Allows traversal in both directions with single pointer field
- Saves memory compared to doubly linked lists
</details>
</details>
</details>

<details>
<summary><strong>3. Tree-based Data Structures</strong></summary>

<details>
<summary><strong>3.1 Binary Trees</strong></summary>

<details>
<summary><strong>Basic Binary Trees</strong></summary>

- Each node has at most two children (left and right)
- Simple recursive structure
- Foundation for more complex tree structures
- Example node:
  ```csharp
  public class TreeNode<T> {
      public T Data { get; set; }
      public TreeNode<T> Left { get; set; }
      public TreeNode<T> Right { get; set; }
      
      public TreeNode(T data) {
          Data = data;
          Left = null;
          Right = null;
      }
  }
  ```
</details>

<details>
<summary><strong>Binary Search Trees</strong></summary>

#### Implementation
- Ordered binary tree where:
  - Left child < Parent
  - Right child > Parent
- Allows efficient searching, insertion, and deletion
- Average case: O(log n) for all operations
- Worst case: O(n) if tree becomes unbalanced

#### Traversal Methods
- **In-order**: Left, Root, Right
  - Visits nodes in ascending order
  - Example: `TraverseInOrder(root.Left); Visit(root); TraverseInOrder(root.Right);`
- **Pre-order**: Root, Left, Right
  - Useful for creating a copy of the tree
  - Example: `Visit(root); TraversePreOrder(root.Left); TraversePreOrder(root.Right);`
- **Post-order**: Left, Right, Root
  - Useful for deleting a tree or evaluating expressions
  - Example: `TraversePostOrder(root.Left); TraversePostOrder(root.Right); Visit(root);`
</details>

<details>
<summary><strong>Balanced Trees</strong></summary>

#### AVL Trees
- Self-balancing binary search tree
- Height difference between left and right subtrees ≤ 1
- Uses rotation operations to maintain balance
- Guarantees O(log n) operations
- Higher overhead than red-black trees for insertions/deletions

#### Red-Black Trees
- Self-balancing binary search tree
- Each node is either red or black
- Balance rules:
  - Root is black
  - No red node has a red child
  - Every path from root to leaf has same number of black nodes
- Less rigidly balanced than AVL, fewer rotations
- Used in many C# collections (e.g., SortedDictionary)
</details>
</details>

<details>
<summary><strong>3.2 Multi-way Trees</strong></summary>

<details>
<summary><strong>B-Trees</strong></summary>

- Self-balancing tree with multiple keys per node
- Designed for efficient disk access (block storage)
- All leaf nodes at same level
- Used in databases and file systems
</details>

<details>
<summary><strong>B+ Trees</strong></summary>

- Variant of B-tree where:
  - Only leaf nodes store data
  - Leaf nodes are linked for sequential access
  - Internal nodes store copies of keys for navigation
- Optimized for range queries and disk-based storage
</details>

<details>
<summary><strong>2-3 Trees</strong></summary>

- Each node has 2 or 3 children
- All leaf nodes at same depth
- Simpler than B-trees but still self-balancing
</details>

<details>
<summary><strong>2-3-4 Trees</strong></summary>

- Each node can have 2, 3, or 4 children
- Equivalent to red-black trees (1-to-1 mapping)
- Self-balancing, all operations O(log n)
</details>
</details>

<details>
<summary><strong>3.3 Specialized Trees</strong></summary>

<details>
<summary><strong>Tries (Prefix Trees)</strong></summary>

- Tree for storing strings
- Each node represents a character
- Path from root forms a string
- Efficient for prefix matching and autocomplete
- Example:
  ```csharp
  public class TrieNode {
      public Dictionary<char, TrieNode> Children { get; set; }
      public bool IsEndOfWord { get; set; }
      
      public TrieNode() {
          Children = new Dictionary<char, TrieNode>();
          IsEndOfWord = false;
      }
  }
  ```
</details>

<details>
<summary><strong>Radix Trees</strong></summary>

- Compressed version of trie
- Collapses single-child nodes
- More space-efficient than regular tries
- Used in IP routing and longest prefix matching
</details>

<details>
<summary><strong>Suffix Trees</strong></summary>

- Specialized for substring searches
- Contains all suffixes of a string
- Enables O(m) substring search (where m is substring length)
- Applications in text processing, bioinformatics
</details>

<details>
<summary><strong>Quad Trees</strong></summary>

- Each node has exactly 4 children
- Used for 2D space partitioning
- Applications in image processing, collision detection
</details>

<details>
<summary><strong>Octrees</strong></summary>

- 3D version of quad tree
- Each node has 8 children
- Used for 3D space partitioning
- Applications in 3D graphics, game physics
</details>
</details>
</details>

<details>
<summary><strong>4. Graph Data Structures</strong></summary>

<details>
<summary><strong>4.1 Graph Representations</strong></summary>

<details>
<summary><strong>Adjacency Matrix</strong></summary>

- 2D array where matrix[i][j] indicates edge from i to j
- Fast edge lookup: O(1)
- Memory usage: O(V²) where V is number of vertices
- Inefficient for sparse graphs
- Example:
  ```csharp
  bool[,] adjacencyMatrix = new bool[vertexCount, vertexCount];
  adjacencyMatrix[0, 1] = true; // Edge from vertex 0 to 1
  ```
</details>

<details>
<summary><strong>Adjacency List</strong></summary>

- Array of lists, each representing connections from a vertex
- Memory-efficient for sparse graphs: O(V+E)
- Vertex lookup: O(degree(v))
- Most commonly used representation
- Example:
  ```csharp
  List<int>[] adjacencyList = new List<int>[vertexCount];
  for (int i = 0; i < vertexCount; i++)
      adjacencyList[i] = new List<int>();
  adjacencyList[0].Add(1); // Edge from vertex 0 to 1
  ```
</details>

<details>
<summary><strong>Incidence Matrix</strong></summary>

- Matrix of vertices × edges
- Each column represents an edge
- Each row represents a vertex
- Entry (i,j) indicates if vertex i is incident on edge j
- Useful for algorithms that work directly with edges
</details>
</details>

<details>
<summary><strong>4.2 Graph Types</strong></summary>

<details>
<summary><strong>Directed Graphs (Digraphs)</strong></summary>

- Edges have direction
- Edge (u,v) is distinct from (v,u)
- Applications: network flows, precedence constraints
</details>

<details>
<summary><strong>Undirected Graphs</strong></summary>

- Edges have no direction
- Edge (u,v) is identical to (v,u)
- Applications: social networks, road maps
</details>

<details>
<summary><strong>Weighted Graphs</strong></summary>

- Edges have associated weights/costs
- Used in shortest path algorithms
- Example:
  ```csharp
  Dictionary<int, double>[] weightedAdjList = new Dictionary<int, double>[vertexCount];
  for (int i = 0; i < vertexCount; i++)
      weightedAdjList[i] = new Dictionary<int, double>();
  weightedAdjList[0][1] = 2.5; // Edge from 0 to 1 with weight 2.5
  ```
</details>

<details>
<summary><strong>Directed Acyclic Graphs (DAGs)</strong></summary>

- Directed graph with no cycles
- Many applications: scheduling, dependency resolution
- Supports topological sorting
</details>
</details>

<details>
<summary><strong>4.3 Graph Operations</strong></summary>

<details>
<summary><strong>Graph Traversal (BFS, DFS)</strong></summary>

#### Breadth-First Search (BFS)
- Uses queue to visit neighbors before going deeper
- Finds shortest paths in unweighted graphs
- Example:
  ```csharp
  Queue<int> queue = new Queue<int>();
  bool[] visited = new bool[vertexCount];
  queue.Enqueue(startVertex);
  visited[startVertex] = true;
  
  while (queue.Count > 0) {
      int v = queue.Dequeue();
      // Process v
      foreach (int neighbor in adjacencyList[v]) {
          if (!visited[neighbor]) {
              visited[neighbor] = true;
              queue.Enqueue(neighbor);
          }
      }
  }
  ```

#### Depth-First Search (DFS)
- Uses stack (or recursion) to explore as far as possible first
- Applications: cycle detection, topological sorting
- Example:
  ```csharp
  void DFS(int vertex, bool[] visited) {
      visited[vertex] = true;
      // Process vertex
      foreach (int neighbor in adjacencyList[vertex]) {
          if (!visited[neighbor]) {
              DFS(neighbor, visited);
          }
      }
  }
  ```
</details>

<details>
<summary><strong>Minimum Spanning Trees</strong></summary>

- Subset of edges connecting all vertices with minimum total weight
- Algorithms:
  - Kruskal's Algorithm: Greedy approach using disjoint-set
  - Prim's Algorithm: Grows tree from a starting vertex
- Applications: network design, clustering
</details>

<details>
<summary><strong>Shortest Path Algorithms</strong></summary>

- Finding minimum cost paths between vertices
- Algorithms:
  - Dijkstra's Algorithm: For graphs with non-negative weights
  - Bellman-Ford: Handles negative weights
  - Floyd-Warshall: All pairs shortest paths
- Applications: routing, navigation
</details>
</details>
</details>

<details>
<summary><strong>5. Advanced Data Structures</strong></summary>

<details>
<summary><strong>5.1 Heaps and Priority Structures</strong></summary>

<details>
<summary><strong>Priority Queues</strong></summary>

- Abstract data type where elements have priorities
- Highest (or lowest) priority element is accessed first
- C# implementation: PriorityQueue<TElement, TPriority>
- Common operations: Enqueue, Dequeue, Peek
- Implementation typically uses binary heap
</details>

<details>
<summary><strong>Binary Heaps</strong></summary>

#### Min Heap
- Complete binary tree where each node ≤ its children
- Root is the minimum element
- Efficient implementation using array
- Operations:
  - Insert: O(log n)
  - ExtractMin: O(log n)
  - FindMin: O(1)

#### Max Heap
- Complete binary tree where each node ≥ its children
- Root is the maximum element
- Uses same implementation as min heap with inverted comparison
- Used for heap sort, finding k largest elements
</details>

<details>
<summary><strong>Fibonacci Heaps</strong></summary>

- More complex heap implementation
- Better amortized bounds for some operations
- Theoretical improvement over binary heaps
- Used in optimization algorithms like Dijkstra's
</details>
</details>

<details>
<summary><strong>5.2 Probabilistic Data Structures</strong></summary>

<details>
<summary><strong>Bloom Filters</strong></summary>

- Space-efficient probabilistic set membership test
- Can result in false positives but never false negatives
- Uses multiple hash functions
- Applications: caching, spell checking, web crawling
</details>

<details>
<summary><strong>Count-Min Sketch</strong></summary>

- Estimates frequency of elements in a stream
- Compact representation using multiple hash functions
- Always provides approximate results
- Applications: frequency counting in large data streams
</details>

<details>
<summary><strong>HyperLogLog</strong></summary>

- Estimates cardinality (count of distinct elements)
- Very memory efficient (sub-linear in cardinality)
- Applications: analytics, database query optimization
</details>
</details>

<details>
<summary><strong>5.3 Specialized Data Structures</strong></summary>

<details>
<summary><strong>Disjoint Set (Union-Find)</strong></summary>

- Keeps track of elements partitioned into disjoint sets
- Operations: Find, Union
- Optimizations: path compression, union by rank
- Applications: Kruskal's algorithm, connected components
</details>

<details>
<summary><strong>Segment Trees</strong></summary>

- Tree for storing intervals or segments
- Efficient range queries
- Operations: O(log n) for query and update
- Applications: range minimum/maximum queries
</details>

<details>
<summary><strong>Fenwick Trees (Binary Indexed Trees)</strong></summary>

- Efficiently updates elements and calculates prefix sums
- More compact than segment trees for some operations
- Applications: frequency tables, range sum queries
</details>

<details>
<summary><strong>Sparse Tables</strong></summary>

- Precomputed data structure for range queries
- O(1) for immutable range queries
- Applications: Range Minimum Query (RMQ)
</details>

<details>
<summary><strong>Interval Trees</strong></summary>

- Stores intervals efficiently
- Fast intersection queries
- Applications: calendar systems, genomic data analysis
</details>
</details>
</details>

## Getting Started

Navigate to each folder to explore specific data structures, or follow the structured learning path outlined in the documentation.

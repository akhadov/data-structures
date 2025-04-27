# C# Data Structures

<details>
# <summary><span style="color:#0d47a1;">Arrays</span>/collapse</summary>

#### <span style="color:blue">Declaration</span>
```csharp
// Single-dimensional array
type[] arrayName;

// Multi-dimensional array
type[,] arrayName;

// Jagged array (array of arrays)
type[][] arrayName;
```

#### <span style="color:blue">Initialization</span>
```csharp
// Single-dimensional array
int[] numbers = new int[5];  // Creates array of 5 integers with default values
int[] numbers = new int[] { 1, 2, 3, 4, 5 };  // Creates and initializes
int[] numbers = { 1, 2, 3, 4, 5 };  // Shorthand initialization

// Multi-dimensional array
int[,] matrix = new int[3, 4];  // Creates a 3x4 array
int[,] matrix = { { 1, 2, 3 }, { 4, 5, 6 } };  // 2x3 array

// Jagged array
int[][] jaggedArray = new int[3][];
jaggedArray[0] = new int[] { 1, 2, 3 };
jaggedArray[1] = new int[] { 4, 5 };
jaggedArray[2] = new int[] { 6, 7, 8, 9 };
```

#### <span style="color:blue">Accessing Elements</span>
```csharp
// Single-dimensional array
int value = numbers[0];  // Access the first element
numbers[0] = 10;        // Modify the first element

// Multi-dimensional array
int value = matrix[1, 2];  // Access element at row 1, column 2
matrix[1, 2] = 15;        // Modify element at row 1, column 2

// Jagged array
int value = jaggedArray[0][1];  // Access second element of first array
jaggedArray[0][1] = 20;         // Modify second element of first array
```

#### <span style="color:blue">Adding and Removing Elements</span>
```csharp
// Arrays in C# have fixed size after creation, so to "add" or "remove" elements:

// To add elements (requires creating a new array)
int[] numbers = { 1, 2, 3 };
int[] newNumbers = new int[numbers.Length + 1];
Array.Copy(numbers, newNumbers, numbers.Length);
newNumbers[newNumbers.Length - 1] = 4;  // Add new element at the end

// Alternative approach using Resize
Array.Resize(ref numbers, numbers.Length + 1);
numbers[numbers.Length - 1] = 4;

// To remove elements (requires creating a new array)
int indexToRemove = 1;
int[] smallerArray = new int[numbers.Length - 1];
Array.Copy(numbers, 0, smallerArray, 0, indexToRemove);
Array.Copy(numbers, indexToRemove + 1, smallerArray, indexToRemove, numbers.Length - indexToRemove - 1);
```

#### <span style="color:green">Methods</span>

<details>
<summary><span style="color:blue">Array.Sort()</span></summary>

```csharp
// Sort array in ascending order
int[] numbers = { 5, 2, 8, 1, 3 };
Array.Sort(numbers);
// Result: numbers = { 1, 2, 3, 5, 8 }

// Sort with custom comparison
Array.Sort(numbers, (a, b) => b.CompareTo(a));  // Descending order
// Result: numbers = { 8, 5, 3, 2, 1 }

// Sort one array based on another
string[] names = { "Alice", "Bob", "Charlie" };
int[] ages = { 30, 25, 35 };
Array.Sort(ages, names);  // Sort names based on ages
// Result: names = { "Bob", "Alice", "Charlie" }, ages = { 25, 30, 35 }
```
</details>

<details>
<summary><span style="color:blue">Array.Reverse()</span></summary>

```csharp
// Reverse entire array
int[] numbers = { 1, 2, 3, 4, 5 };
Array.Reverse(numbers);
// Result: numbers = { 5, 4, 3, 2, 1 }

// Reverse portion of array
int[] values = { 1, 2, 3, 4, 5, 6 };
Array.Reverse(values, 1, 3);  // Reverse 3 elements starting at index 1
// Result: values = { 1, 4, 3, 2, 5, 6 }
```
</details>

<details>
<summary><span style="color:blue">Array.Clear()</span></summary>

```csharp
// Clear entire array (set to default values)
int[] numbers = { 1, 2, 3, 4, 5 };
Array.Clear(numbers, 0, numbers.Length);
// Result: numbers = { 0, 0, 0, 0, 0 }

// Clear portion of array
string[] names = { "Alice", "Bob", "Charlie", "David" };
Array.Clear(names, 1, 2);  // Clear 2 elements starting at index 1
// Result: names = { "Alice", null, null, "David" }
```
</details>

<details>
<summary><span style="color:blue">Array.Copy()</span></summary>

```csharp
// Copy entire array
int[] source = { 1, 2, 3, 4, 5 };
int[] destination = new int[source.Length];
Array.Copy(source, destination, source.Length);
// Result: destination = { 1, 2, 3, 4, 5 }

// Copy portion of array
int[] partial = new int[3];
Array.Copy(source, 1, partial, 0, 3);
// Result: partial = { 2, 3, 4 }
```
</details>

<details>
<summary><span style="color:blue">Array.IndexOf() / LastIndexOf()</span></summary>

```csharp
// Find first occurrence
int[] numbers = { 10, 20, 30, 20, 40 };
int firstIndex = Array.IndexOf(numbers, 20);
// Result: firstIndex = 1

// Find last occurrence
int lastIndex = Array.LastIndexOf(numbers, 20);
// Result: lastIndex = 3

// Find in a specific range
int rangeIndex = Array.IndexOf(numbers, 20, 2);  // Start from index 2
// Result: rangeIndex = 3
```
</details>

<details>
<summary><span style="color:blue">Array.Resize()</span></summary>

```csharp
// Increase array size
int[] numbers = { 1, 2, 3 };
Array.Resize(ref numbers, 5);
// Result: numbers = { 1, 2, 3, 0, 0 }

// Decrease array size (truncates elements)
int[] values = { 10, 20, 30, 40, 50 };
Array.Resize(ref values, 3);
// Result: values = { 10, 20, 30 }
```
</details>

<details>
<summary><span style="color:blue">Array.Find() / FindAll()</span></summary>

```csharp
// Find first matching element
int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8 };
int firstEven = Array.Find(numbers, n => n % 2 == 0);
// Result: firstEven = 2

// Find all matching elements
int[] allEvens = Array.FindAll(numbers, n => n % 2 == 0);
// Result: allEvens = { 2, 4, 6, 8 }

// Find first or default
int greaterThanTen = Array.Find(numbers, n => n > 10);
// Result: greaterThanTen = 0 (default for int since no element > 10)
```
</details>

<details>
<summary><span style="color:blue">Array.Exists() / TrueForAll()</span></summary>

```csharp
// Check if any element satisfies a condition
int[] numbers = { 1, 2, 3, 4, 5 };
bool hasEven = Array.Exists(numbers, n => n % 2 == 0);
// Result: hasEven = true

// Check if all elements satisfy a condition
bool allPositive = Array.TrueForAll(numbers, n => n > 0);
// Result: allPositive = true
```
</details>

<details>
<summary><span style="color:blue">Array.ConvertAll()</span></summary>

```csharp
// Convert array elements to different type
int[] numbers = { 1, 2, 3, 4, 5 };
string[] stringNumbers = Array.ConvertAll(numbers, n => n.ToString());
// Result: stringNumbers = { "1", "2", "3", "4", "5" }

// Convert to computed values
double[] doubles = Array.ConvertAll(numbers, n => n * 1.5);
// Result: doubles = { 1.5, 3.0, 4.5, 6.0, 7.5 }
```
</details>

#### <span style="color:blue">Properties</span>

<details>
<summary><span style="color:blue">Array Properties</span></summary>

```csharp
// Get array length
int[] numbers = { 1, 2, 3, 4, 5 };
int length = numbers.Length;  // length = 5

// Get array rank (number of dimensions)
int[,] matrix = new int[3, 4];
int rank = matrix.Rank;  // rank = 2

// Get length of specific dimension
int rows = matrix.GetLength(0);  // rows = 3
int cols = matrix.GetLength(1);  // cols = 4

// Get lower and upper bounds
int lowerBound = matrix.GetLowerBound(0);  // Usually 0
int upperBound = matrix.GetUpperBound(0);  // Usually length-1
```
</details>

</details>

### Lists

### Dictionaries
- HashSets
  - HashSet<T>
  - SortedSet<T>

### FIFO/LIFO Collections
- Queues
- Stacks
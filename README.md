# C# Data Structures

<details>
<summary><span>$\Large\color{#4FC3F7}{Arrays}$</span></summary>

#### <span>$\large\color{#4FC3F7}{Declaration}$</span>
```csharp
// Single-dimensional array
type[] arrayName;

// Multi-dimensional array
type[,] arrayName;

// Jagged array (array of arrays)
type[][] arrayName;
```

#### <span>$\large\color{#4FC3F7}{Initialization}$</span>
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

#### <span>$\large\color{#4FC3F7}{Accessing Elements}$</span>
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

#### <span>$\large\color{#4FC3F7}{Adding and Removing Elements}$</span>
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

#### <span>$\large\color{#f5750e}{Methods}$</span>

<details>
<summary><span>$\color{#f5750e}{Array.Sort()}$</span></summary>

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
<summary><span>$\color{#f5750e}{Array.Reverse()}$</span></summary>

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
<summary><span>$\color{#f5750e}{Array.Clear()}$</span></summary>

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
<summary><span>$\color{#f5750e}{Array.Copy()}$</span></summary>

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
<summary><span>$\color{#f5750e}{Array.IndexOf() / LastIndexOf()}$</span></summary>

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
<summary><span>$\color{#f5750e}{Array.Resize()}$</span></summary>

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
<summary><span>$\color{#f5750e}{Array.Find() / FindAll()}$</span></summary>

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
<summary><span>$\color{#f5750e}{Array.Exists() / TrueForAll()}$</span></summary>

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
<summary><span>$\color{#f5750e}{Array.ConvertAll()}$</span></summary>

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

#### <span>$\large\color{#4FC3F7}{Properties}$</span>

<details>
<summary><span>$\color{#4FC3F7}{Array Properties}$</span></summary>

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

<details>
<summary><span>$\Large\color{#4FC3F7}{Lists}$</span></summary>

#### <span>$\large\color{#4FC3F7}{Declaration}$</span>
```csharp
// Generic List
List<type> listName;

// Examples
List<int> numbers;
List<string> names;
List<Person> people;  // Custom type
```

#### <span>$\large\color{#4FC3F7}{Initialization}$</span>
```csharp
// Empty list
List<int> numbers = new List<int>();

// List with initial capacity
List<string> names = new List<string>(10);  // Space for 10 items

// Initialize with values
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Initialize from an array or collection
int[] array = { 1, 2, 3 };
List<int> numbers = new List<int>(array);
```

#### <span>$\large\color{#4FC3F7}{Accessing Elements}$</span>
```csharp
// Access by index
List<string> fruits = new List<string> { "Apple", "Banana", "Cherry" };
string fruit = fruits[1];  // "Banana"

// Modify by index
fruits[1] = "Blueberry";  // Change "Banana" to "Blueberry"

// Check if an index is valid
if (index >= 0 && index < fruits.Count)
{
    // Safe to access fruits[index]
}
```

#### <span>$\large\color{#4FC3F7}{Adding and Removing Elements}$</span>
```csharp
List<string> fruits = new List<string>();

// Add elements
fruits.Add("Apple");           // Add single item
fruits.AddRange(new[] { "Banana", "Cherry" });  // Add multiple items

// Insert at specific position
fruits.Insert(1, "Blueberry");  // Insert at index 1
fruits.InsertRange(2, new[] { "Mango", "Orange" });  // Insert multiple at index 2

// Remove elements
fruits.Remove("Banana");           // Remove by value (first occurrence)
fruits.RemoveAt(0);                // Remove by index
fruits.RemoveRange(1, 2);          // Remove range (start index, count)
fruits.RemoveAll(f => f.Length < 6);  // Remove all matching a condition

// Clear the list
fruits.Clear();  // Remove all elements
```

#### <span>$\large\color{#f5750e}{Methods}$</span>

<details>
<summary><span>$\color{#f5750e}{List<T>.Find() / FindAll()}$</span></summary>

```csharp
List<int> numbers = new List<int> { 5, 12, 8, 15, 3, 20 };

// Find first matching element
int first = numbers.Find(n => n > 10);  // Returns 12

// Find last matching element
int last = numbers.FindLast(n => n > 10);  // Returns 20

// Find all matching elements
List<int> matches = numbers.FindAll(n => n > 10);  // Returns { 12, 15, 20 }

// Find by index
int index = numbers.FindIndex(n => n > 10);  // Returns 1 (index of 12)
int lastIndex = numbers.FindLastIndex(n => n > 10);  // Returns 5 (index of 20)

// Find with start index and count
int indexInRange = numbers.FindIndex(2, 3, n => n > 10);  // Starts at index 2, checks 3 items
```
</details>

<details>
<summary><span>$\color{#f5750e}{List<T>.Sort()}$</span></summary>

```csharp
List<int> numbers = new List<int> { 5, 2, 8, 1, 3 };

// Sort entire list in ascending order
numbers.Sort();  // Results in { 1, 2, 3, 5, 8 }

// Sort with custom comparison
numbers.Sort((a, b) => b.CompareTo(a));  // Descending order, results in { 8, 5, 3, 2, 1 }

// Sort using a Comparison delegate
numbers.Sort(delegate(int x, int y) { return x.CompareTo(y); });

// Sort using a Comparer
numbers.Sort(Comparer<int>.Default);

// Sort a range (index, count)
numbers = new List<int> { 5, 2, 8, 1, 3, 9 };
numbers.Sort(1, 3, Comparer<int>.Default);  // Sort only items at index 1, 2, 3
```
</details>

<details>
<summary><span>$\color{#f5750e}{List<T>.Contains() / Exists()}$</span></summary>

```csharp
List<string> fruits = new List<string> { "Apple", "Banana", "Cherry" };

// Check if list contains an element
bool hasApple = fruits.Contains("Apple");  // true
bool hasOrange = fruits.Contains("Orange");  // false

// Check with custom equality comparer
bool hasAppleIgnoreCase = fruits.Contains("apple", StringComparer.OrdinalIgnoreCase);  // true

// Check using a predicate
bool hasA = fruits.Exists(f => f.StartsWith("A"));  // true
bool longFruit = fruits.Exists(f => f.Length > 10);  // false
```
</details>

<details>
<summary><span>$\color{#f5750e}{List<T>.ForEach()}$</span></summary>

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Apply action to each element
numbers.ForEach(n => Console.WriteLine(n));

// Modify each element
numbers.ForEach(n => n *= 2);  // Note: This doesn't actually modify the list items!

// To modify each element
for (int i = 0; i < numbers.Count; i++)
{
    numbers[i] *= 2;
}

// Or using a more complex action
numbers.ForEach(delegate(int n) {
    Console.WriteLine($"Processing {n}");
    // More operations...
});
```
</details>

<details>
<summary><span>$\color{#f5750e}{List<T>.ConvertAll()}$</span></summary>

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Convert to a different type
List<string> strings = numbers.ConvertAll(n => n.ToString());
// Result: { "1", "2", "3", "4", "5" }

// Transform values
List<int> squared = numbers.ConvertAll(n => n * n);
// Result: { 1, 4, 9, 16, 25 }

// Convert to a complex type
List<Person> people = numbers.ConvertAll(n => new Person { Id = n, Name = $"Person {n}" });
```
</details>

<details>
<summary><span>$\color{#f5750e}{List<T>.GetRange()}$</span></summary>

```csharp
List<int> numbers = new List<int> { 10, 20, 30, 40, 50, 60 };

// Get a range of elements
List<int> subset = numbers.GetRange(1, 3);  // Start at index 1, get 3 items
// Result: { 20, 30, 40 }

// Clone a list
List<int> clone = numbers.GetRange(0, numbers.Count);

// Use GetRange with other methods
numbers.GetRange(2, 2).ForEach(Console.WriteLine);  // Print items at index 2 and 3
```
</details>

<details>
<summary><span>$\color{#f5750e}{List<T>.BinarySearch()}$</span></summary>

```csharp
List<int> numbers = new List<int> { 10, 20, 30, 40, 50 };  // Must be sorted!

// Find item index
int index = numbers.BinarySearch(30);  // Returns 2

// If item not found, returns bitwise complement of the next larger item index
int notFound = numbers.BinarySearch(35);  // Returns ~3 (complement of 3)

// Convert negative result to insertion point
if (index < 0)
    index = ~index;  // Where the item should be inserted

// Search with custom comparison
index = numbers.BinarySearch(25, Comparer<int>.Default);

// Search a range (index, count)
index = numbers.BinarySearch(1, 3, 40, null);  // Search in items 1, 2, 3
```
</details>

<details>
<summary><span>$\color{#f5750e}{List<T>.TrueForAll()}$</span></summary>

```csharp
List<int> numbers = new List<int> { 2, 4, 6, 8, 10 };

// Check if all elements satisfy a condition
bool allEven = numbers.TrueForAll(n => n % 2 == 0);  // true
bool allGreaterThan5 = numbers.TrueForAll(n => n > 5);  // false

// Combining conditions
bool validList = numbers.TrueForAll(n => n > 0 && n % 2 == 0);  // true
```
</details>

<details>
<summary><span>$\color{#f5750e}{List<T>.IndexOf() / LastIndexOf()}$</span></summary>

```csharp
List<string> colors = new List<string> { "Red", "Green", "Blue", "Green", "Yellow" };

// Find first occurrence
int firstGreen = colors.IndexOf("Green");  // Returns 1

// Find last occurrence
int lastGreen = colors.LastIndexOf("Green");  // Returns 3

// Find with start index
int fromIndex = colors.IndexOf("Green", 2);  // Returns 3 (search starts at index 2)

// Find with start index and count
int inRange = colors.IndexOf("Green", 0, 2);  // Returns 1 (search first 2 items)

// Case insensitive search
int ignoreCase = colors.FindIndex(c => c.Equals("red", StringComparison.OrdinalIgnoreCase));  // Returns 0
```
</details>

#### <span>$\large\color{#4FC3F7}{Properties}$</span>

<details>
<summary><span>$\color{#4FC3F7}{List<T> Properties}$</span></summary>

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Get item count
int count = numbers.Count;  // 5

// Get capacity (internal array size)
int capacity = numbers.Capacity;  // Could be larger than Count

// Set capacity explicitly
numbers.Capacity = 10;  // Allocates space for 10 items

// Optimize memory usage
numbers.TrimExcess();  // Reduces capacity to match Count (if difference is significant)
```
</details>

</details>

### Dictionaries
- HashSets
  - HashSet<T>
  - SortedSet<T>

### FIFO/LIFO Collections
- Queues
- Stacks
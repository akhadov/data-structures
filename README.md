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

<details>
<summary><span>$\Large\color{#4FC3F7}{Dictionaries}$</span></summary>

#### <span>$\large\color{#4FC3F7}{Declaration}$</span>
```csharp
// Generic Dictionary
Dictionary<TKey, TValue> dictionaryName;

// Examples
Dictionary<int, string> employeeIds;
Dictionary<string, decimal> prices;
Dictionary<string, List<string>> categoryItems;  // Complex value type
Dictionary<Person, Address> peopleAddresses;    // Custom types
```

#### <span>$\large\color{#4FC3F7}{Initialization}$</span>
```csharp
// Empty dictionary
Dictionary<int, string> employees = new Dictionary<int, string>();

// Dictionary with initial capacity
Dictionary<string, decimal> prices = new Dictionary<string, decimal>(100);  // Space for 100 items

// Initialize with custom comparer
Dictionary<string, int> scores = new Dictionary<string, int>(StringComparer.OrdinalIgnoreCase);

// Initialize with values
Dictionary<int, string> employees = new Dictionary<int, string>
{
    { 101, "John Doe" },
    { 102, "Jane Smith" },
    { 103, "Tom Brown" }
};

// Alternative initialization syntax
Dictionary<int, string> employees = new Dictionary<int, string>
{
    [101] = "John Doe",
    [102] = "Jane Smith",
    [103] = "Tom Brown"
};

// Initialize from collection of KeyValuePair
List<KeyValuePair<int, string>> pairs = GetKeyValuePairs();
Dictionary<int, string> fromPairs = new Dictionary<int, string>(pairs);
```

#### <span>$\large\color{#4FC3F7}{Accessing Elements}$</span>
```csharp
Dictionary<int, string> employees = new Dictionary<int, string>
{
    { 101, "John Doe" },
    { 102, "Jane Smith" }
};

// Access by key (throws KeyNotFoundException if key doesn't exist)
string employee = employees[101];  // "John Doe"

// Safely check and access
if (employees.ContainsKey(103))
{
    string employee = employees[103];
}

// Using TryGetValue (preferred method)
if (employees.TryGetValue(102, out string name))
{
    Console.WriteLine(name);  // "Jane Smith"
}

// Modifying values
employees[101] = "John Smith";  // Update existing value

// Adding new entries
employees[104] = "Alice Johnson";  // Add new key-value pair
```

#### <span>$\large\color{#4FC3F7}{Adding and Removing Elements}$</span>
```csharp
Dictionary<string, decimal> prices = new Dictionary<string, decimal>();

// Add elements
prices.Add("Apple", 1.99m);  // Add single item
// prices.Add("Apple", 2.49m);  // Would throw exception - key already exists

// Check before adding
if (!prices.ContainsKey("Banana"))
{
    prices.Add("Banana", 0.99m);
}

// Adding or updating (upsert)
prices["Banana"] = 1.29m;  // Updates if exists, adds if not

// Alternative safe add/update with TryAdd (.NET 5+)
prices.TryAdd("Cherry", 3.49m);  // Returns false if key exists, doesn't throw

// Remove elements
prices.Remove("Apple");  // Remove by key, returns true if successful

// Try to remove and get the value
if (prices.Remove("Banana", out decimal bananaPrice))
{
    Console.WriteLine($"Removed Banana that cost {bananaPrice}");
}

// Clear the dictionary
prices.Clear();  // Remove all elements
```

#### <span>$\large\color{#f5750e}{Methods}$</span>

<details>
<summary><span>$\color{#f5750e}{Dictionary<TKey, TValue>.ContainsKey() / ContainsValue()}$</span></summary>

```csharp
Dictionary<string, int> scores = new Dictionary<string, int>
{
    { "Alice", 95 },
    { "Bob", 80 },
    { "Charlie", 95 }
};

// Check if dictionary contains a key
bool hasAlice = scores.ContainsKey("Alice");  // true
bool hasDave = scores.ContainsKey("Dave");    // false

// Check if dictionary contains a value
bool has95 = scores.ContainsValue(95);   // true
bool has100 = scores.ContainsValue(100); // false

// Note: ContainsValue is O(n) operation, searches through all values
```
</details>

<details>
<summary><span>$\color{#f5750e}{Dictionary<TKey, TValue>.TryGetValue()}$</span></summary>

```csharp
Dictionary<string, int> ages = new Dictionary<string, int>
{
    { "Alice", 25 },
    { "Bob", 30 }
};

// Safe way to get a value without exceptions
if (ages.TryGetValue("Alice", out int aliceAge))
{
    Console.WriteLine($"Alice is {aliceAge} years old");  // Alice is 25 years old
}

// When key doesn't exist
if (!ages.TryGetValue("Charlie", out int charlieAge))
{
    Console.WriteLine("Charlie not found");  // Charlie not found
    // Note: charlieAge is set to default(int) which is 0
}

// Inline usage with null-coalescing operator
int bobAge = ages.TryGetValue("Bob", out int age) ? age : -1;  // 30
```
</details>

<details>
<summary><span>$\color{#f5750e}{Dictionary<TKey, TValue>.Keys / Values}$</span></summary>

```csharp
Dictionary<int, string> employees = new Dictionary<int, string>
{
    { 101, "John" },
    { 102, "Jane" },
    { 103, "Bob" }
};

// Get all keys
ICollection<int> keys = employees.Keys;  // Collection of { 101, 102, 103 }
foreach (int id in keys)
{
    Console.WriteLine($"Employee ID: {id}");
}

// Get all values
ICollection<string> names = employees.Values;  // Collection of { "John", "Jane", "Bob" }
foreach (string name in names)
{
    Console.WriteLine($"Employee name: {name}");
}

// Convert keys or values to arrays/lists
int[] idArray = employees.Keys.ToArray();
List<string> nameList = employees.Values.ToList();
```
</details>

<details>
<summary><span>$\color{#f5750e}{Dictionary<TKey, TValue>.GetEnumerator()}$</span></summary>

```csharp
Dictionary<string, decimal> prices = new Dictionary<string, decimal>
{
    { "Apple", 1.99m },
    { "Banana", 0.99m },
    { "Orange", 2.49m }
};

// Iterate through key-value pairs
foreach (KeyValuePair<string, decimal> item in prices)
{
    Console.WriteLine($"{item.Key}: ${item.Value}");
}

// Deconstruction in C# 7.0+
foreach (var (fruit, price) in prices)
{
    Console.WriteLine($"{fruit}: ${price}");
}

// Using enumerator directly
using (Dictionary<string, decimal>.Enumerator enumerator = prices.GetEnumerator())
{
    while (enumerator.MoveNext())
    {
        KeyValuePair<string, decimal> current = enumerator.Current;
        Console.WriteLine($"{current.Key}: ${current.Value}");
    }
}
```
</details>

<details>
<summary><span>$\color{#f5750e}{Dictionary<TKey, TValue>.EnsureCapacity() / TrimExcess()}$</span></summary>

```csharp
// Memory optimization methods (.NET Core 2.0+ / .NET 5+)
Dictionary<int, string> largeDict = new Dictionary<int, string>();

// Ensure capacity before adding many items
largeDict.EnsureCapacity(10000);  // Pre-allocate space for efficiency

// Add many items
for (int i = 0; i < 10000; i++)
{
    largeDict[i] = $"Item {i}";
}

// Remove many items
for (int i = 0; i < 8000; i++)
{
    largeDict.Remove(i);
}

// Trim excess capacity after removing items
largeDict.TrimExcess();  // Reduce memory usage
```
</details>

<details>
<summary><span>$\color{#f5750e}{Dictionary<TKey, TValue> LINQ Extensions}$</span></summary>

```csharp
Dictionary<string, int> scores = new Dictionary<string, int>
{
    { "Alice", 95 },
    { "Bob", 80 },
    { "Charlie", 95 },
    { "David", 65 }
};

// Filter with LINQ
var highScores = scores.Where(kv => kv.Value >= 90)
                      .ToDictionary(kv => kv.Key, kv => kv.Value);
// Result: { "Alice": 95, "Charlie": 95 }

// Transform with LINQ
var letterGrades = scores.ToDictionary(
    kv => kv.Key,
    kv => kv.Value >= 90 ? "A" : kv.Value >= 80 ? "B" : kv.Value >= 70 ? "C" : "D"
);
// Result: { "Alice": "A", "Bob": "B", "Charlie": "A", "David": "D" }

// Group by value
var groupedByScore = scores.GroupBy(kv => kv.Value)
                          .ToDictionary(g => g.Key, g => g.Select(kv => kv.Key).ToList());
// Result: { 95: ["Alice", "Charlie"], 80: ["Bob"], 65: ["David"] }
```
</details>

<details>
<summary><span>$\color{#f5750e}{Dictionary<TKey, TValue> Specialized Operations}$</span></summary>

```csharp
// Merging dictionaries
Dictionary<string, int> dict1 = new Dictionary<string, int> { { "A", 1 }, { "B", 2 } };
Dictionary<string, int> dict2 = new Dictionary<string, int> { { "B", 3 }, { "C", 4 } };

// Method 1: Loop through second dictionary (B gets overwritten)
foreach (var item in dict2)
{
    dict1[item.Key] = item.Value;
}
// Result: dict1 = { "A": 1, "B": 3, "C": 4 }

// Method 2: Only add keys that don't exist
foreach (var item in dict2)
{
    if (!dict1.ContainsKey(item.Key))
    {
        dict1[item.Key] = item.Value;
    }
}

// Copying a dictionary
Dictionary<string, int> copy = new Dictionary<string, int>(dict1);

// Comparing dictionaries
bool areEqual = dict1.Count == dict2.Count &&
                !dict1.Except(dict2).Any();
```
</details>

#### <span>$\large\color{#4FC3F7}{Properties}$</span>

<details>
<summary><span>$\color{#4FC3F7}{Dictionary<TKey, TValue> Properties}$</span></summary>

```csharp
Dictionary<string, int> scores = new Dictionary<string, int>
{
    { "Alice", 95 },
    { "Bob", 80 },
    { "Charlie", 95 }
};

// Get item count
int count = scores.Count;  // 3

// Get key collection
ICollection<string> keys = scores.Keys;

// Get value collection
ICollection<int> values = scores.Values;

// Get the comparer being used
IEqualityComparer<string> comparer = scores.Comparer;

// Check if dictionary is read-only
bool isReadOnly = ((ICollection<KeyValuePair<string, int>>)scores).IsReadOnly;  // False
```
</details>

</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{HashSets}$</span></summary>
- HashSet<T>
- SortedSet<T>
</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{FIFO/LIFO Collections}$</span></summary>
- Queue<T>
- Stack<T>
</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{Linked Lists}$</span></summary>
- LinkedList<T>
- LinkedListNode<T>
</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{Sorted Collections}$</span></summary>
- SortedList<TKey, TValue>
- SortedDictionary<TKey, TValue>
</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{Concurrent Collections}$</span></summary>
- ConcurrentDictionary<TKey, TValue>
- ConcurrentQueue<T>
- ConcurrentStack<T>
- ConcurrentBag<T>
- BlockingCollection<T>
</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{Immutable Collections}$</span></summary>
- ImmutableArray<T>
- ImmutableList<T>
- ImmutableDictionary<TKey, TValue>
- ImmutableHashSet<T>
- ImmutableQueue<T>
- ImmutableStack<T>
</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{Observable Collections}$</span></summary>
- ObservableCollection<T>
</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{Special Collections}$</span></summary>
- ReadOnlyCollection<T>
- BitArray
- NameValueCollection
</details>

<details>
<summary><span>$\Large\color{#4FC3F7}{Custom Data Structures}$</span></summary>
- Priority Queue (built-in with .NET 6+)
- Circular Buffer
- Trie
- Graph
</details>
# CollectionsAndGenerics

# Data Structures in C# – When and How to Use Them

This README provides an overview of several common data structures in C#, explains when to use each one, and discusses their algorithmic complexities using Big O notation.
It also includes code examples for each data structure and a comparison of lookup performance in a List (with LINQ) versus a Dictionary.

## Arrays

**Characteristics:**
- **Fixed size:** Once an array is created, its length cannot be changed.
- **Contiguous memory:** Fast random access with O(1) indexing.
- **Best for:** When the number of elements is known ahead of time.

**Big O Complexity:**
- **Access by index:** O(1)
- **Insertion/Deletion (if shifting is needed):** O(n)

**Example:**
```csharp
// Declare and initialize an array of integers with fixed size
int[] numbers = new int[] { 1, 2, 3, 4, 5 };

// Accessing an element (O(1))
Console.WriteLine(numbers[2]); // Output: 3

// To "add" more elements, you must create a new array:
int[] largerArray = new int[numbers.Length + 1];
Array.Copy(numbers, largerArray, numbers.Length);
largerArray[numbers.Length] = 6;
```

**Application:**
- **Storing Data:** Ideal for storing and managing collections of variables that have a fixed size or whose size changes infrequently.
- **Lookup Tables:** Arrays can efficiently implement lookup tables, enabling rapid access to precomputed values.
- **Implementing Other Data Structures:** The underlying structure for more complex data structures like heaps, hash tables, and dynamic arrays.
- **Algorithms:** Used in a wide range of algorithms, including sorting and searching algorithms, where random access to elements significantly optimizes performance.


## List<T>

A List uses an internal array to store data.Whenever the List becomes full the size of the array inside it is doubled(times * 2)
inorder to accomodate more data.

```csharp
// Implements a variable-size List that uses an array of objects to store the
    // elements. A List has a capacity, which is the allocated length
    // of the internal array. As elements are added to a List, the capacity
    // of the List is automatically increased as required by reallocating the
    // internal array.
    //
    [DebuggerTypeProxy(typeof(ICollectionDebugView<>))]
    [DebuggerDisplay("Count = {Count}")]
    [Serializable]
    [TypeForwardedFrom("mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089")]
    public class List<T> : IList<T>, IList, IReadOnlyList<T>
```

**Characteristics:**
- **Dynamic resizing:** A List<T> can grow or shrink as needed.
- **Indexable:** Provides fast random access similar to arrays.
- **Best for:** When you need a collection that changes size at runtime.
 
**Big O Complexity:**

- **Access by index:** O(1)
- **Insertion at the end:** O(1) amortized (occasionally O(n) during resizing)
- **Insertion/Deletion in the middle:** O(n) (due to shifting elements)

**Example:**
```csharp
// Create and initialize a List of integers
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Add an element (amortized O(1))
numbers.Add(6);

// Access an element by index (O(1))
Console.WriteLine(numbers[2]); // Output: 3
```

## Dictionary<TKey, TValue>

**Characteristics:**
- **Key-value pairs:** Stores data as unique key and value pairs.
- **Hash table implementation:** Offers fast average-case lookups.
- **Best for:** When you need to quickly retrieve data based on a unique key.
 
**Big O Complexity:**

- **Lookup, Insertion, Deletion (average-case):** O(1)
- **ookup, Insertion, Deletion (worst-case due to hash collisions):** O(n).

**Example:**
```csharp
// Create and initialize a Dictionary
Dictionary<int, string> students = new Dictionary<int, string>
{
    { 1, "Alice" },
    { 2, "Bob" },
    { 3, "Charlie" }
};

// Retrieve a value by key (O(1))
Console.WriteLine(students[2]); // Output: Bob

// Add a new key-value pair (O(1))
students[4] = "David";

// Remove a key-value pair (O(1))
students.Remove(1);
```

## HashSet<T>

**Characteristics:**
- **Unique elements only:** Duplicate values are not allowed.
- **Fast lookups:** Uses a hash table internally.
- **Best for:** storing unique elements and checking existence quickly.

**Big O Complexity:**

- **Lookup, Insertion, Deletion (average-case):** O(1)
- **Lookup, Insertion, Deletion (worst-case due to hash collisions):** O(n).

**Example:**
```csharp
// Create and initialize a HashSet
HashSet<int> numbers = new HashSet<int> { 1, 2, 3, 4, 5 };

// Add elements (O(1))
numbers.Add(6);

// Check if an element exists (O(1))
Console.WriteLine(numbers.Contains(3)); // Output: True

// Remove an element (O(1))
numbers.Remove(2);
```





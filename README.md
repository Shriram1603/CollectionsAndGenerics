# CollectionsAndGenerics

# Data Structures in C# – When and How to Use Them

This README provides an overview of several common data structures in C#, explains when to use each one, and discusses their algorithmic complexities using Big O notation.

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
- **Lookup, Insertion, Deletion (worst-case due to hash collisions):** O(n).

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

## Queue<T>

**Characteristics:**
- **FIFO (First-In, First-Out):**  Elements are processed in the order they were added.
- **Best for:** Scenarios where elements should be processed in order.

**Big O Complexity:**

- **Enqueue (adding element):** O(1)
- **Dequeue (Removing element):** O(1)
- **Peeking (viewing the front element):** O(1).

**Example:**
```csharp
// Create and initialize a Queue
Queue<string> customers = new Queue<string>();

// Enqueue elements (O(1))
customers.Enqueue("Alice");
customers.Enqueue("Bob");
customers.Enqueue("Charlie");

// Peek at the front element (O(1))
Console.WriteLine(customers.Peek()); // Output: Alice

// Dequeue (O(1))
customers.Dequeue(); // Removes "Alice"

```

**Use Cases:**

- **Job Scheduling:** Operating systems use queues to manage processes and tasks that need to be executed, scheduling them in the order they arrive.
- **Handling Requests:** Web servers use queues to handle incoming request traffic, processing each request in the order it was received.
- **Data Streaming:** In streaming data applications, queues can be used to buffer data chunks before they are processed, ensuring that they are dealt with in the correct order.
- **Breadth-First Search (BFS):** In graph algorithms, queues are used to traverse the graph level by level, starting from a given node.


## Stack<T>

**Characteristics:**
- **LIFO (Last-In, First-Out):**  The last element added is the first to be removed.
- **Best for:** Scenarios that require reversing order or backtracking.

**Big O Complexity:**

- **Push (adding element):** O(1)
- **Pop (adding element):** O(1)
- **Peeking (viewing the top element):** O(1).

**Example:**
```csharp
// Create and initialize a Stack
Stack<int> stack = new Stack<int>();

// Push elements (O(1))
stack.Push(1);
stack.Push(2);
stack.Push(3);

// Peek at the top element (O(1))
Console.WriteLine(stack.Peek()); // Output: 3

// Pop elements (O(1))
stack.Pop(); // Removes 3
```

**Use Cases:**

- **Function Call Management:** Stacks are used by programming languages to manage function calls. When a function is called, its execution context is pushed onto a call stack, and when the function returns, its context is popped off.
- **Undo Mechanisms:** Many applications use stacks to keep track of actions for undo operations. Each action is pushed onto a stack, and undoing an action pops it off the stack and reverses it.
- **Syntax Parsing:** Compilers and interpreters use stacks for parsing and evaluating expressions or checking the syntax of code with nested structures like parentheses.
- **Backtracking:** In algorithms that involve searching or traversing through possible solutions (like maze solving), stacks are used to keep track of the path taken and backtrack if necessary.


## LinkedList<T>

**Characteristics:**
- **Doubly linked:**  Each node has references to the previous and next nodes.
- **Best for:** Frequent insertions and deletions in the middle of a list.

**Big O Complexity:**

- **Insertion/Deletion at beginning or end: ** O(1)
- **Access by index: ** O(n)
- **Insertion/Deletion in the middle:** O(n) (finding the position takes O(n)).

**Example:**
```csharp
// Create and initialize a LinkedList
LinkedList<int> numbers = new LinkedList<int>();

// Add elements at the beginning and end (O(1))
numbers.AddFirst(1);
numbers.AddLast(2);
numbers.AddLast(3);

// Insert after a specific node (O(1) if reference is known)
LinkedListNode<int> node = numbers.Find(1);
numbers.AddAfter(node, 5);

// Remove an element (O(1) if reference is known)
numbers.Remove(2);
```

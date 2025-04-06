Alright, let's move on to **Topic 4: Stacks**. Stacks are a fundamental abstract data type and a linear data structure that follows a very specific principle for adding and removing elements.

### What is a Stack?

A **stack** is a collection of elements that operates on the **LIFO (Last-In, First-Out)** principle. This means the _last_ element added to the stack will be the _first_ element removed.

**Analogy: A Stack of Plates**

Imagine a stack of plates in a cafeteria dispenser:

- You can only add a new clean plate to the **top** of the stack.
- You can only take a plate from the **top** of the stack.
- You can't easily take a plate from the middle or bottom without removing the ones above it first.

The last plate placed on top is the first one taken off.

**Analogy: Browser Back Button**

Think about your web browser's history for the back button:

- When you visit a new page, it's added to the "top" of the history stack for that tab.
- When you press the "Back" button, the _most recently visited_ page (the one at the top) is removed, and you go to the page that's now at the top.

### Core Operations

Stacks primarily support three main operations:

1. **Push:** Adds a new element to the **top** of the stack.
   - _Analogy:_ Placing a new plate on top of the stack.
2. **Pop:** Removes the **topmost** element from the stack and usually returns it. An error or exception occurs if you try to pop from an empty stack (underflow).
   - _Analogy:_ Taking the top plate off the stack.
3. **Peek (or Top):** Returns the value of the **topmost** element _without_ removing it. Useful for checking what's next without modifying the stack. An error might occur if the stack is empty.
   - _Analogy:_ Looking at the top plate without taking it.

Other possible operations include:

- **isEmpty:** Checks if the stack contains any elements. Returns true if empty, false otherwise.
- **size:** Returns the number of elements currently in the stack.

### Implementation

Stacks are an _abstract data type (ADT)_ – they define _what_ operations can be performed (Push, Pop, Peek) and the LIFO behavior, but not _how_ they are implemented internally. Two common ways to implement a stack are using Arrays (or Dynamic Arrays) and Linked Lists.

**1. Implementation using Arrays (or Dynamic Arrays):**

- **How it works:**
  - Use an array (let's say `stackArray`) to store the elements.
  - Maintain an integer variable `topIndex` (or `size`) that points to the index of the top element (or the next available slot). Initially, `topIndex` might be -1 or 0, depending on the convention.
- **Operations:**
  - **Push(element):**
    1. Increment `topIndex`.
    2. Place `element` at `stackArray[topIndex]`.
    3. (If using dynamic array) Check if the array is full; if so, resize it _before_ inserting.
  - **Pop():**
    1. Check for underflow (e.g., if `topIndex` is -1).
    2. Get the element at `stackArray[topIndex]`.
    3. Decrement `topIndex`.
    4. Return the element.
    5. (Optional: Clear the popped slot `stackArray[topIndex+1] = null` to allow garbage collection if needed).
  - **Peek():**
    1. Check if empty.
    2. Return the element at `stackArray[topIndex]`.
- **Pros:**
  - Simple to implement.
  - Good memory locality (elements are contiguous), potentially faster iteration (though stack iteration is uncommon).
- **Cons:**
  - **Fixed Size (Static Array):** Can lead to overflow if the stack grows beyond the array capacity.
  - **Resizing Overhead (Dynamic Array):** If using a dynamic array, push operations can occasionally take O(n) time when resizing occurs (though it's O(1) _amortized_ time).

**2. Implementation using Linked Lists (Singly Linked List):**

- **How it works:**
  - Use a singly linked list where the `head` of the list represents the **top** of the stack.
- **Operations:**
  - **Push(element):**
    1. Create a `newNode` with the `element`.
    2. Set `newNode.next` to point to the current `head`.
    3. Update `head` to point to `newNode`. (This is exactly the O(1) "insert at head" operation for linked lists).
  - **Pop():**
    1. Check for underflow (if `head` is null).
    2. Store the data from the `head` node (`head.data`).
    3. Update `head` to point to `head.next`. (This is exactly the O(1) "delete head" operation for linked lists).
    4. Return the stored data.
  - **Peek():**
    1. Check if empty (`head` is null).
    2. Return `head.data`.
- **Pros:**
  - **Truly Dynamic Size:** Never overflows due to size limitations (only limited by available system memory). No resizing overhead.
- **Cons:**
  - **Memory Overhead:** Each element requires extra memory for the `next` pointer compared to arrays.
  - **No Random Access:** Not really a con for stacks, as you _only_ operate on the top.

### Time and Space Complexity

For both standard array/dynamic array (amortized) and linked list implementations, the core stack operations have the following complexities:

| Operation | Time Complexity | Space Complexity (Auxiliary, for the operation) |
| :-------- | :-------------- | :---------------------------------------------- |
| Push      | O(1) \*         | O(1)                                            |
| Pop       | O(1)            | O(1)                                            |
| Peek      | O(1)            | O(1)                                            |
| isEmpty   | O(1)            | O(1)                                            |
| size      | O(1)            | O(1)                                            |

\* _O(1) amortized for dynamic arrays (due to potential resizing), strictly O(1) for linked lists and fixed-size arrays (until full)._

The **overall space complexity** of the stack itself is **O(n)**, where `n` is the number of elements stored, as it needs space to hold the elements.

### Common Applications

Stacks are used in many areas of computer science:

1. **Function Call Management:** When you call a function, its local variables and return address are pushed onto the call stack. When the function returns, its frame is popped off. This is how nested calls and recursion work.
2. **Expression Evaluation:** Converting infix expressions (like `3 + 4 * 2`) to postfix (like `3 4 2 * +`) and evaluating postfix expressions.
3. **Syntax Parsing:** Compilers use stacks to check if parentheses, braces, and brackets match correctly in code.
4. **Undo/Redo Functionality:** Text editors and other programs often use stacks to keep track of actions performed, allowing you to "undo" by popping the last action or "redo" by pushing it back.
5. **Backtracking Algorithms:** Used in algorithms that explore possibilities and need to backtrack if a path leads to a dead end (e.g., solving mazes, N-Queens problem). The stack keeps track of the path taken.
6. **Depth-First Search (DFS):** An algorithm for traversing graph or tree data structures can be implemented iteratively using a stack.

---

So, stacks are simple but powerful structures defined by their LIFO behavior. They offer constant-time push, pop, and peek operations and can be implemented efficiently using either arrays or linked lists, each with minor trade-offs.

**Does the LIFO concept, the core operations, the implementation methods (array vs. linked list), and the applications make sense? Any questions about stacks?**

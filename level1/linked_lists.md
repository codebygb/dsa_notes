Okay, let's move on to **Topic 3: Linked Lists**. This data structure offers a different approach to storing sequential data compared to arrays, with its own set of trade-offs.

### What is a Linked List?

A **linked list** is a linear data structure where elements are _not_ stored in contiguous memory locations. Instead, each element, called a **node**, contains two pieces of information:

1. **Data:** The actual value or item being stored (e.g., a number, a string, an object).
2. **Pointer/Reference (Next):** A link or address that points to the _next_ node in the sequence.

The list is formed by linking these nodes together like a chain. The entry point to the list is usually a pointer called the **head**, which points to the very first node. The last node in the list typically has its `next` pointer set to `null` (or some special marker) to indicate the end of the list.

**Analogy: A Treasure Hunt**

Think of a treasure hunt:

- Each **clue (node)** contains:
  - Some information or part of the treasure (**data**).
  - Instructions telling you where to find the _next_ clue (**next pointer**).
- You start with the **first clue (head)**.
- You follow the instructions on each clue to get to the next one.
- The **last clue** tells you you've found the treasure and doesn't point anywhere else (**next pointer is null**).

Unlike arrays (houses on a numbered street), the clues (nodes) could be hidden anywhere; it's the _link_ from one clue to the next that defines the order, not their physical location.

### Node Structure

The basic building block is the **Node**:

```
Node {
  data      // Stores the value
  next      // Pointer/reference to the next Node in the list
}
```

### Types of Linked Lists

1. **Singly Linked List:** The most basic type. Each node has only _one_ pointer (`next`) pointing to the subsequent node. You can only traverse the list in one direction (forward).
2. **Doubly Linked List:** Each node has _two_ pointers:
   - `next`: Points to the next node.
   - `prev`: Points to the _previous_ node.
     This allows traversal in both forward and backward directions.
3. **Circular Linked List:** The `next` pointer of the _last_ node points back to the `head` node, forming a circle. Can be singly or doubly linked.

_We'll focus primarily on Singly Linked Lists first, then touch on Doubly._

### Basic Operations (Singly Linked List)

Let `n` be the number of nodes in the list.

1. **Traversal:**

   - **Operation:** Visit each node in the list, usually starting from the head.
   - **How it works:** Start with a temporary pointer (`current`) set to `head`. While `current` is not `null`, process `current.data`, then update `current` to `current.next`.
   - **Time Complexity: O(n)** - You need to visit every node.
   - **Space Complexity: O(1)** - Only requires a few temporary pointers.

2. **Search (by Value):**

   - **Operation:** Find the first node containing a specific value.
   - **How it works:** Traverse the list (as above), comparing `current.data` with the target value. Return the node (or true) if found, or continue until the end.
   - **Time Complexity: O(n)** - In the worst case, the value is the last node or not present, requiring traversal of the entire list.
   - **Space Complexity: O(1)**

3. **Insertion:**

   - **Case 1: Inserting at the Head:**
     - **How it works:**
       1. Create a `newNode` with the desired data.
       2. Set `newNode.next` to point to the current `head`.
       3. Update the `head` of the list to point to `newNode`.
     - **Time Complexity: O(1)** - Very fast, just involves rearranging a couple of pointers.
   - **Case 2: Inserting at the Tail (End):**
     - **How it works (without a tail pointer):**
       1. Create a `newNode`, set `newNode.next` to `null`.
       2. Traverse the list until you find the _last_ node (where `current.next` is `null`). This takes O(n) time.
       3. Set `lastNode.next` to point to `newNode`.
     - **Time Complexity: O(n)** - Dominated by the traversal to find the last node.
     - **How it works (with a tail pointer):** If the list maintains an extra pointer `tail` to the last node:
       1. Create `newNode`, set `newNode.next` to `null`.
       2. Set `tail.next` to point to `newNode`.
       3. Update `tail` to point to `newNode`.
     - **Time Complexity: O(1)** - Fast if a tail pointer is maintained.
   - **Case 3: Inserting in the Middle (e.g., after a given node `prevNode`):**
     - **How it works:**
       1. Create `newNode`.
       2. Set `newNode.next` to point to `prevNode.next`.
       3. Set `prevNode.next` to point to `newNode`.
     - **Time Complexity:** Finding `prevNode` might take O(n) if searching by value, but the insertion _itself_ (once you have `prevNode`) is **O(1)**.

4. **Deletion:**
   - **Case 1: Deleting the Head:**
     - **How it works:**
       1. Check if the list is empty.
       2. Update `head` to point to `head.next`.
     - **Time Complexity: O(1)** - Very fast.
   - **Case 2: Deleting the Tail (End):**
     - **How it works (Singly Linked List):**
       1. You need to find the _second-to-last_ node to update its `next` pointer to `null`.
       2. Traverse the list keeping track of the `previous` and `current` node. Stop when `current.next` is `null`. The `previous` node is the second-to-last.
       3. Set `previous.next` to `null`.
     - **Time Complexity: O(n)** - Requires traversal.
   - **Case 3: Deleting in the Middle (e.g., node _after_ `prevNode`):**
     - **How it works:**
       1. Let `nodeToDelete = prevNode.next`.
       2. Set `prevNode.next` to `nodeToDelete.next` (or `prevNode.next.next`). This bypasses `nodeToDelete`.
     - **Time Complexity:** Finding `prevNode` might take O(n), but the deletion _itself_ (once you have `prevNode`) is **O(1)**.
     - **Important:** To delete a node `X` in a singly linked list, you generally need a pointer to the node _before_ `X`.

### Time Complexity Summary (Singly Linked List)

| Operation                    | Time Complexity (Worst Case) | Space Complexity (Auxiliary) | Array Comparison (Worst Case Time) |
| :--------------------------- | :--------------------------- | :--------------------------- | :--------------------------------- |
| Access/Search by Index/Value | O(n)                         | O(1)                         | O(1) / O(n)                        |
| Insertion at Head            | O(1)                         | O(1)                         | O(n)                               |
| Insertion at Tail            | O(n) / O(1)\*                | O(1)                         | O(1)                               |
| Insertion in Middle          | O(n) \*\*                    | O(1)                         | O(n)                               |
| Deletion at Head             | O(1)                         | O(1)                         | O(n)                               |
| Deletion at Tail             | O(n)                         | O(1)                         | O(1)                               |
| Deletion in Middle           | O(n) \*\*                    | O(1)                         | O(n)                               |

\* _O(1) if a tail pointer is maintained, O(n) otherwise._
\*\* _O(n) typically includes finding the location; the pointer manipulation itself is O(1)._

### Doubly Linked Lists

- **Node:** `Node { data, next, prev }`
- **Benefit:** Can traverse backwards. Deletion of a specific node `X` is O(1) _if you have a pointer directly to node `X`_ (because you can access its `prev` node using `X.prev` to update pointers). Deletion at the tail also becomes O(1) if a `tail` pointer is maintained.
- **Drawback:** Requires more memory per node (for the `prev` pointer). Insertions and deletions are slightly more complex as you need to update both `next` and `prev` pointers carefully.

### Advantages of Linked Lists (vs. Arrays)

1. **Dynamic Size:** Easily grow and shrink without resizing overhead (like dynamic arrays sometimes have).
2. **Efficient Insertions/Deletions (at beginning/known positions):** Inserting/deleting at the head is O(1). Inserting/deleting in the middle/end is O(1) _if you already have a pointer to the relevant node(s)_ (e.g., the node before). This contrasts sharply with arrays' O(n) cost for these operations due to shifting.

### Disadvantages of Linked Lists (vs. Arrays)

1. **No Random Access / Slow Access by Index:** To get to the i-th element, you _must_ start at the head and follow `i` `next` pointers. This takes O(n) time, whereas arrays offer O(1) indexed access.
2. **Slow Search:** Searching for a value requires traversing the list, taking O(n) time on average/worst case (same as unsorted arrays, but sorted arrays allow O(log n) search).
3. **Higher Memory Overhead:** Each node requires extra memory for the `next` pointer (and `prev` in doubly linked lists), which can be significant compared to arrays storing just the data.
4. **More Complex Pointer Management:** Requires careful handling of pointers during insertions/deletions to avoid breaking the list structure.

---

Linked lists provide flexibility in size and fast insertions/deletions at the cost of direct access and search speed. They are useful when you have frequent additions/removals and don't need fast indexed access.

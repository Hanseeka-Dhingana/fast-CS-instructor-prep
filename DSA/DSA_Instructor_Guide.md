# Data Structures and Algorithms - Instructor Study Guide

This guide covers the core topics from the CSC-222 syllabus, structured to help you review for your instructor job test.

## 1. Elementary Data Structures: Arrays
* **Core Concept:** A linear collection of elements stored in contiguous memory locations.
* **Key Teaching Points:** * O(1) time complexity for index-based access.
    * Limitations: Fixed size (in static arrays) and expensive insertions/deletions O(n) because elements must be shifted.
    * Multi-dimensional arrays (like 2D matrices) map to 1D contiguous memory in row-major or column-major order.

## 2. Linked Lists
* **Core Concept:** A linear collection where elements (nodes) are stored non-contiguously. Each node contains data and a reference (pointer) to the next node.
* **Variations:**
    * **Singly Linked:** One direction traversal.
    * **Doubly Linked:** Contains 'next' and 'previous' pointers; allows bidirectional traversal but requires more memory per node.
    * **Circular Linked:** The last node points back to the head, creating a loop. Useful for round-robin scheduling.
* **Key Teaching Points:** Efficient O(1) insertions/deletions at known positions (like the head), but O(n) access/search time. 

## 3. Stacks (LIFO)
* **Core Concept:** Last-In-First-Out data structure. Think of a stack of plates.
* **Operations:** `Push` (add to top), `Pop` (remove from top).
* **Key Teaching Points:** Often implemented using arrays or linked lists. Crucial for understanding function call stacks (recursion), undo mechanisms, and expression parsing.

## 4. Queues (FIFO)
* **Core Concept:** First-In-First-Out data structure. Think of a line at a grocery store.
* **Operations:** `Enqueue` (add to rear), `Dequeue` (remove from front).
* **Variations:**
    * **Circular Queue:** Solves the "wasted space" problem of array-based queues by wrapping the rear index back to the start.
    * **Priority Queue:** Elements are removed based on priority, not arrival time (usually implemented with Heaps).

## 5. Algorithm Analysis & Big O Notation
* **Core Concept:** Evaluating the efficiency of algorithms independent of hardware.
* **Key Teaching Points:** * **Time Complexity:** How runtime scales with input size (n).
    * **Space Complexity:** How memory usage scales with input size (n).
    * Big O notation represents the worst-case scenario (upper bound). You should also be comfortable discussing average and best-case analysis.

## 6. Trees & Heaps
* **Core Concept:** A hierarchical, non-linear structure consisting of nodes and edges.
* **Terminology:** Root, Leaf, Parent, Child, Height, Depth.
* **Max-Heap:** A complete binary tree where every parent node is greater than or equal to its children. Perfect for priority queues.

## 7. Binary Search Trees (BST)
* **Core Concept:** A binary tree where the left child is smaller than the parent, and the right child is greater.
* **Key Teaching Points:** * Fast O(log n) average time for search, insert, and delete.
    * **Worst-case pitfall:** If elements are inserted in sorted order, it degrades into a linked list with O(n) time complexity.
    * **Traversals:** Inorder (yields sorted elements), Preorder, Postorder.

## 8. AVL Trees
* **Core Concept:** A self-balancing Binary Search Tree.
* **Key Teaching Points:** Prevents the O(n) worst-case of standard BSTs. It maintains a "Balance Factor" (-1, 0, or 1) for every node. If the balance factor is violated, it uses Rotations (LL, RR, LR, RL) to rebalance.

## 9. Sorting Algorithms
* **Bubble Sort:** Swaps adjacent elements. O(n^2). Good for teaching, bad for production.
* **Selection Sort:** Selects the minimum element and places it at the front. O(n^2).
* **Insertion Sort:** Builds a sorted subarray one element at a time. O(n^2).
* **Merge Sort:** Divide and conquer. Splits array, sorts halves, merges them. O(n log n). Requires O(n) extra space.

## 10. Hashing
* **Core Concept:** Maps keys to specific array indices using a hash function for O(1) average lookup time.
* **Key Teaching Points:** * **Collisions:** What happens when two keys hash to the same index.
    * **Chain based scheme (Chaining):** Each array index holds a linked list of elements that hashed to that spot.

## 11. Graphs
* **Core Concept:** A set of vertices (nodes) connected by edges. Can be directed/undirected, weighted/unweighted.
* **Traversals:**
    * **BFS (Breadth-First Search):** Explores level-by-level using a Queue. Good for finding shortest paths in unweighted graphs.
    * **DFS (Depth-First Search):** Explores branch-by-branch using a Stack (or recursion). Good for maze solving or topological sorting.
* **Spanning Tree:** A subset of edges that connects all vertices without any cycles.

# Data Structures & Algorithms - Quick Revision Guide



# Elementary Data Structures:  
## 1. Arrays
* **Concept:** Contiguous memory locations storing elements of the same type.
* **Types:** 1D arrays (lists), 2D arrays (matrices), Multi-dimensional arrays.
* **Limitations:** Fixed size, contiguous memory requirement, expensive insertions and deletions.

## 2. Linked Lists
* **Concept:** Non-contiguous memory allocation where each element (node) contains data and a pointer to the next node.
* **Types:** * Singly Linked List: Traverse in one direction.
    * Circular Singly Linked List: Last node points to the head.
    * Doubly Linked List: Nodes have pointers to both next and previous nodes.
    * Circular Doubly Linked List: Last node points to head, head's previous points to last.
* **Operations:** Traversing, inserting (head, any location), searching, removing (head, anywhere), reversing using recursion.

## 3. Queues (FIFO)
* **Concept:** First-In-First-Out (FIFO) structure.
* **Representations:** Array-based (can lead to wasted space without circular implementation), Dynamic/Linked List based.
* **Circular Queue:** Solves the wasted space issue in array representation by wrapping around to the beginning.
* **Priority Queues:** Elements are dequeued based on priority rather than arrival time.

## 4. Stacks (LIFO)
* **Concept:** Last-In-First-Out (LIFO) structure.
* **Operations:** Push (add to top), Pop (remove from top).
* **Implementation:** Using arrays or linked lists.
* **Applications:** Reversing a list, parsing expressions, function call management (recursion).

## 5. Analysis of Algorithms
* **Complexity:** Measuring algorithm efficiency.
    * **Time Complexity:** How execution time scales with input size.
    * **Space Complexity:** How memory usage scales with input size.
* **Big O Notation:** Upper bound of an algorithm's complexity. Evaluated via Best-case, Worst-case, and Average-case analysis.

## 6. Trees & Priority Queues (Heaps)
* **Terminology:** Root, Parent, Child, Leaf, Depth, Height.
* **Binary Trees:** Each node has at most two children. Includes Complete Binary Trees.
* **Heaps:** A complete binary tree used to implement priority queues. 
    * Max-Heap: Parent is greater than or equal to its children.

## 7. Binary Search Trees (BST)
* **Concept:** Left child is smaller than parent; right child is greater.
* **Operations:** Finding, inserting, and deleting nodes (handles 3 cases: leaf node, one child, two children).
* **Traversals:** * Inorder (Left, Root, Right) - Gives sorted order.
    * Preorder (Root, Left, Right).
    * Postorder (Left, Right, Root).
* **Efficiency:** Average time complexity is O(log n), but worst-case (unbalanced) degrades to O(n).

## 8. AVL Trees
* **Concept:** A self-balancing Binary Search Tree.
* **Balance Factor:** Height of Left Subtree - Height of Right Subtree (must be -1, 0, or 1).
* **Rotations:** Uses 4 cases (Left-Left, Right-Right, Left-Right, Right-Left) to maintain balance during insertions/deletions.

## 9. Sorting Algorithms
* **Bubble Sort:** Repeatedly swaps adjacent elements if they are in the wrong order. O(n^2).
* **Selection Sort:** Repeatedly finds the minimum element from the unsorted part and puts it at the beginning. O(n^2).
* **Insertion Sort:** Builds the sorted array one element at a time by comparing and shifting. O(n^2).
* **Merge Sort:** Divide and conquer algorithm that splits the array in half, sorts, and merges. O(n log n).

## 10. Hashing
* **Concept:** Maps keys to values for highly efficient lookups.
* **Hash Tables:** Uses a hash function to compute an index into an array of buckets or slots.
* **Collision Handling:** * Chain based scheme (Chaining): Each slot holds a linked list of entries.

## 11. Graphs
* **Concept:** Nodes (vertices) connected by edges. Can be directed or undirected, weighted or unweighted.
* **Traversals:** * BFS (Breadth-First Search): Explores neighbor nodes first (uses Queue).
    * DFS (Depth-First Search): Explores as far as possible along each branch before backtracking (uses Stack).
* **Spanning Tree:** A subgraph that includes all vertices of the graph with the minimum possible number of edges.




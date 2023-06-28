---
title: "The 'O' Complexity (cheat-sheet)"
datePublished: Tue Jun 06 2023 06:17:36 GMT+0000 (Coordinated Universal Time)
cuid: clijw2nca000709l3aovd03wy
slug: the-o-complexity-cheat-sheet
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/3V8xo5Gbusk/upload/66ffe4a25a8859c604220bd4d3236b9a.jpeg
tags: java, data-structures, cheatsheet, dsa

---

In this blog post, we will see time complexity and delve into the average time complexities of various common data structures for insertion, deletion, and traversal operations. Understanding these complexities will empower you to make informed decisions when choosing the right data structure for your specific use case, ultimately leading to more efficient and scalable code.

For each data structure, we will explore the average time complexities associated with insertion, deletion, and traversal operations. It is important to note that the time complexities mentioned are averages and may vary in certain scenarios.

By the end of this blog post, you will have a solid understanding of how different data structures perform when it comes to these essential operations, enabling you to choose the most suitable data structure for your specific needs. So, let's dive in and unlock the world of time complexity in data structures!

1. **<mark>Array</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686031376415/c143fda2-fe76-4bf0-b9e8-934223161ced.png align="center")
    
    * Insertion: O(n) - Inserting an element at the end of the array takes O(1) on average, but inserting at any other position requires shifting elements and takes O(n) time.
        
    * Deletion: O(n) - Deleting an element from the middle of the array requires shifting elements, resulting in O(n) time complexity.
        
    * Traversal: O(n) - Accessing each element in the array requires visiting each index, so resulting in O(n) time complexity.
        
2. **<mark>Linked List</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686031465211/c86ad109-8eae-4661-b02c-a9e03cf971ae.png align="center")
    
    * Insertion: O(1) - Inserting an element at the beginning or end of a linked list takes constant time on average since it involves updating a few pointers.
        
    * Deletion: O(1) - Deleting an element from the beginning or end of a linked list takes constant time on average as it involves updating a few pointers.
        
    * Traversal: O(n) - Visiting each element in a linked list requires traversing through each node, resulting in O(n) time complexity.
        
3. **<mark>Stack</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686031598007/7d87ada7-9fa1-41dd-878f-75585665b4a7.png align="center")
    
    * Insertion: O(1) - Pushing an element onto a stack takes constant time on average since it involves adding an element to the top of the stack.
        
    * Deletion: O(1) - Popping an element from a stack takes constant time on average as it involves removing the topmost element.
        
    * Traversal: O(n) - To traverse a stack, you need to pop each element until the stack is empty, resulting in O(n) time complexity.
        
4. **<mark>Queue</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686031715504/1f073081-eade-4679-8035-46318ad29542.png align="center")
    
    * Insertion: O(1) - Enqueuing an element into a queue takes constant time on average since it involves adding an element to the end of the queue.
        
    * Deletion: O(1) - Dequeuing an element from a queue takes constant time on average as it involves removing the front element.
        
    * Traversal: O(n) - To traverse a queue, you need to dequeue each element until the queue is empty, resulting in O(n) time complexity.
        
5. **<mark>Binary Search Tree (BST)</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686031790818/dc86243c-3dc9-413e-b509-669a0e2794c7.png align="center")
    
    * Insertion: O(log n) - Inserting an element into a balanced BST takes average logarithmic time as it requires traversing through the height of the tree.
        
    * Deletion: O(log n) - Deleting an element from a balanced BST takes average logarithmic time as it involves searching and updating the tree structure.
        
    * Traversal: O(n) - In-order traversal of BST visits every node once, resulting in O(n) time complexity.
        
6. **<mark>AVL Tree</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686031862100/975cb271-041d-4e5c-9c48-e090eceff73a.png align="center")
    
    * Insertion: O(log n) - Inserting an element into an AVL tree, a self-balancing binary search tree, takes average logarithmic time.
        
    * Deletion: O(log n) - Deleting an element from an AVL tree takes average logarithmic time.
        
    * Searching: O(log n) - Searching for an element in an AVL tree takes average logarithmic time.
        
    * Traversal: O(n) - In-order traversal of an AVL tree visits every node once, resulting in a time complexity of O(n), where n is the number of elements.
        
7. **<mark>Hash Table (HashMap)</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686031953894/4670d1c3-f340-46a2-9514-7328f0519042.png align="center")
    
    * Insertion: O(1) - On average, inserting an element into a hash table takes constant time. However, in the worst case, when there are collisions, the time complexity can be O(n), where n is the number of elements.
        
    * Deletion: O(1) - On average, deleting an element from a hash table takes constant time. In the worst case, it can be O(n) due to collisions.
        
    * Searching: O(1) - On average, searching for an element in a hash table takes constant time. In the worst case, it can be O(n) due to collisions.
        
    * Traversal: O(n) - To traverse all the elements in a hash table, you need to visit each bucket and each element in the bucket, resulting in a time complexity of O(n), where n is the number of elements.
        
8. **<mark>Hash Set (HashSet)</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686032041977/e2055e5a-5d45-492b-9875-6051dbf68dfa.png align="center")
    
    * Insertion: O(1) - On average, inserting an element into a hash set takes constant time.
        
    * Deletion: O(1) - On average, deleting an element from a hash set takes constant time.
        
    * Searching: O(1) - On average, searching for an element in a hash set takes constant time.
        
    * Traversal: O(n) - To traverse all the elements in a hash set, you need to visit each element, resulting in a time complexity of O(n), where n is the number of elements.
        
9. **<mark>Graph (Adjacency Matrix representation)</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686032108630/08c4a213-8527-4b5b-8836-aa461c9a461b.png align="center")
    
    * Insertion: O(1) - Inserting an edge into a graph, represented using an adjacency matrix, takes constant time.
        
    * Deletion: O(1) - Deleting an edge from a graph, represented using an adjacency matrix, takes constant time.
        
    * Searching: O(1) - Searching for an edge in a graph, represented using an adjacency matrix, takes constant time.
        
    * Traversal: O(V^2) - To traverse all the vertices and edges in a graph, represented using an adjacency matrix, takes quadratic time. It involves visiting each entry in the matrix, where V is the number of vertices.
        
10. **<mark>Graph (Adjacency List representation)</mark>**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686032191142/4684ac38-9220-49d7-a5e5-ec6508b558be.png align="center")
    
    * Insertion: O(1) - Inserting an edge into a graph, represented using an adjacency list, takes constant time.
        
    * Deletion: O(V + E) - Deleting an edge from a graph, represented using an adjacency list, takes linear time. It involves searching and removing the edge from the adjacency list of the corresponding vertices.
        
    * Searching: O(V) - Searching for an edge in a graph, represented using an adjacency list, takes linear time. It involves searching the adjacency list of the source vertex.
        
    * Traversal: O(V + E) - Traversing all the vertices and edges in a graph, represented using an adjacency list, takes linear time. It involves visiting each vertex and its adjacent vertices.
        

Please comment out if anything left or yiu want to add in this blog, will be happy to add.
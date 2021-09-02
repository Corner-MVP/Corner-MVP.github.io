---
title: Heap and heapSort
date: 2021-04-07 20:05:48
tags: 
    - Data structure
categories:
    - Data structure and algorithm
---

# Definition

Heap is a kind of complete binary tree. A complete binary tree is a binary tree in which every level, except maybe last level, is full, and all nodes are as far as left as possible.

Commonly, there are two kinds of heap, the one is max-heap, and the other is min-heap.

Max-heap is the heap that parent's value is greater than their children's value, and the parent's value of min-heap is less than their children.

# Operations

## Insert a node

1. Make a new node in the last level, as far left as possible. If the last level is full, make a new one;

2. If the new one breaks heap property, swap with its parent node;

3. Repeat former two steps until every node is satisfied with heap property;

4. Time complexity `O(log H)` H is the height of tree

## Delete a node

1. Remove the root node, and bring the last node (rightmost node in the last level) to the root;

2. If the root breaks heap property, look at its children and swap it with the larger one;

3. Repeat former two steps until no nodes conflict heap property;

4. Time complexity `O(log H)` H is the height of tree


# Implement Max-heap with python

```
class MaxHeap:
    def __init__(self, maxSize=None):
        self.maxSize = maxSize
        self.elements = []
        self.count = 0

    def addNode(self, value):

        if self.count > self.maxSize:
            raise Exception('The heap is full.')

        self.elements.append(value)
        self.siftUp(self.count)
        self.count += 1

    def popNode(self):

        if self.count == 0:
            raise Exception('The heap is empty.')

        value = self.elements[0]
        self.count -= 1
        self.elements[0] = self.elements[self.count]
        self.siftDown(0)
        return value

    def siftUp(self, index):

        if index > 0:
            parent = (index - 1) // 2
            if self.elements[index] > self.elements[parent]:
                self.elements[index], self.elements[parent] = self.elements[parent], self.elements[index]
                self.siftUp(parent)

    def siftDown(self, index):

        left = 2 * index + 1
        right = 2 * index + 2
        largest = index
        if (left <= self.count
                and self.elements[left] >= self.elements[largest]
                and self.elements[left] >= self.elements[right]):
            largest = left

        elif (right < self.count
              and self.elements[right] >= self.elements[largest]):
            largest = right

        if largest != index:
            self.elements[index], self.elements[largest] = self.elements[largest], self.elements[index]
            self.siftDown(largest)
```

# Heap sort

From the above narrate, it is not hard to find no matter max-heap and min-heap, the top of heap is largest or least value of the whole heap, therefore, it

```

    def heapSort(arr):

      length = len(arr)
      heap = MaxHeap(length)

      for item in arr:
        heap.addNode(item)

      res = []
      count = heap.count
      while count > 0:
        node = heap.popNode()
        res.insert(0, node)
        count -= 1

      return res

```

Time complexity `O(N)` N is the length of array
Space complexity `O(N)` N is the length of array


Reference:

1. https://web.stanford.edu/class/cs97si/03-data-structures.pdf

2. https://python-data-structures-and-algorithms.readthedocs.io/zh/latest/15_%E5%A0%86%E4%B8%8E%E5%A0%86%E6%8E%92%E5%BA%8F/heap_and_heapsort/

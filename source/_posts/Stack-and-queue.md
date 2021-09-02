---
title: Stack and queue
date: 2021-04-07 20:03:06
tags: 
    - Data structure
categories:
    - Data structure and algorithm
---

# Definition

**Stack**: Last in, first out (LIFO)

**Queue**: First in, first out (FIFO)

# Operations

## Stack

1. push(x): inserts x into a stack.

2. pop(): removes the newest item from a stack.

3. top(): returns the newest item from a stack.

## Queue

1. Enqueue(x): inserts x into the queue.

2. Dequeue(): removes the oldest item from the queue.

3. Front(): returns the oldest item from the queue.

# Implement with python

## Stack

```
class Stack:
    def __init__(self):
        self.stack = []

    def _push(self, value):
        self.stack.append(value)

    def _pop(self):

        if not self.stack:
            raise Exception('The stack is empty.')
        return self.stack.pop()

    def _top(self):

        if not self.stack:
            raise Exception('The stack is empty.')
        return self.stack[-1]
```

## Queue

```
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, value):
        self.queue.append(value)

    def dequeue(self):

        if not self.queue:
            raise Exception('The queue is empty.')
        return self.queue.pop(0)

    def front(self):
        if not self.queue:
            raise Exception('The queue is empty.')
        return self.queue[0]
```

Reference:

1. https://web.stanford.edu/class/cs97si/03-data-structures.pdf

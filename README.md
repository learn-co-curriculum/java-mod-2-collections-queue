# Queue

## Learning Goals

- Understand the Queue interface
- Use Queue implementations

## Queue in Java

A queue is a specialized collection data structure that adds and removes
elements from its internal data structure in a specific way:

1. New elements are always added to the end of the list
2. Elements are always removed from the beginning of the list

In the most basic implementation of a queue, "beginning of the list" and "end of
the list" are determined by _when_ an element is added to the queue. In other
words, when an element is added to the queue, it's always added at the end of
the queue, and when an element is removed from the queue, it's always removed
from the start of the queue, and the queue is always sorted based on when
elements are added to it.

Queues can be "prioritized" by something other than the time they were added,
however. Java offers the `PriorityQueue` implementation of the `Queue` interface
for example, which by default orders items in the queue based on their natural
ordering, and can also support custom ordering through the `Comparator`
interface.

For this section, however, we will work with the `LinkedList` implementation of
the `Queue` interface, which does order elements based on when they were added
to the queue.

In addition to all the methods we've come to expect from any members of the
`Collections` framework, the `Queue` interface adds the following key methods:

1. `add()` - adds an element to the head of the queue
2. `element()` - returns the element at the head of the queue, _without_
   removing it from the queue, meaning that 2 subsequent calls to the
   `element()` method will return the same element
3. `remove()` - returns the element at the head of the queue, _and_ removes it
   from the queue

```java
        Queue<Integer> myNumbers = new LinkedList<Integer>();
        for (Integer counter = 0; counter < 10; counter++) {
            myNumbers.add(counter);
        }
        while (!myNumbers.isEmpty()) {
            System.out.println(myNumbers.remove());
        }
```

The code above produces the following output:

```plaintext
0
1
2
3
4
5
6
7
8
9
```

As we go through the queue and call `remove()` repeatedly, we continue to reduce
the size of the queue until it is eventually empty, at which point the
`myNumbers.isEmpty()` call returns `false` and the `while` loop ends.

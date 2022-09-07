# Queue

## Learning Goals

- Understand the Queue interface.
- Explain a LinkedList data structure.
- Review commonly used methods.

## Queue in Java

`Queue` is an interface in Java that implements the `Collection` interface and
provides a way to store an ordered collection. It differs from the `List`
interface in that a queue is a specialized collection data structure that adds
and removes elements in a first-in, first-out (FIFO) access pattern. This means,
when we add an element, the element is always added to the end of the queue.
When we remove an element, the element is always removed from the beginning of
the queue. The queue is always sorted based on when elements are added to it.

We can think of a queue as a line in a grocery store. The line is formed by the
order people enter the line. When we are ready to check out, we get in line at
the _end_. When we finish buying our items, we get out of line by exiting the
_beginning_ of the line. The same is true for a `Queue` when it comes to
adding and removing items.

Just like the `List` interface, there are a few implementations of the `Queue`:

1. `LinkedList`: this implementation also implements the `List` interface. It
   is a linear data structure where the elements are linked to each other.
2. `PriorityQueue`: this implementation allows items to be "prioritized" by
   something other than the time the elements were added. For example, a
   priority queue is ordered according to the natural ordering of the elements.
3. `ArrayDeque`: this implementation is also known as an array double ended
   queue or an array deck. It is a resizable array that allows items to be added
   or removed from either side of the queue.

For this section, however, we will work with the `LinkedList` implementation of
the `Queue` interface, which does order elements based on when they were added
to the queue.

## LinkedList in Action

To use a `Queue` in Java, we will need to import it from the `java.util` package
like we did with all our other data structures thus far. Then we will need to
choose an implementation of the `Queue` interface. In this section, we will
discuss the LinkedList. A **LinkedList** is a class that consists of
**nodes**. Each element in a linked list is known as a node that keeps track of
3 fields:

1. A link to the previous element in the list.
2. A link to the next element in the list.
3. The actual data stored in that node.

If an item is the first in the queue, then the node will point to a `null` value
for the previous element. If an item is the last in the queue, then the node
will point to a `null` value for the next element.

Let's look at an example to further illustrate this:

```java
import java.util.Queue;
import java.util.LinkedList;

public class QueueExample {
   public static void main(String[] args) {
      Queue<Integer> myNumbers = new LinkedList<Integer>();

      for (Integer counter = 0; counter < 3; counter++) {
         myNumbers.add(counter);
      }

      while (!myNumbers.isEmpty()) {
         System.out.println(myNumbers.remove());
      }
   }
}
```

The output of the above would be:

```plaintext
0
1
2
```

Now let's look at what this `LinkedList` would look like in terms of how nodes
store the links of the previous and next elements in a queue:

![LinkedList-Initial](https://curriculum-content.s3.amazonaws.com/java-mod-2/queue/LinkedList-Add.png)

In the illustration above, the black arrows are showing the previous links and
the blue arrows are showing the next links.

Let's continue to break this down:

- The first node in the queue is the `Integer` 0.
  - The actual data this node holds is the number 0.
  - The previous node is `null`, indicating that it is the first in the queue
    and there is no node before it. So when we remove a number from the queue,
    this will be the first one to be removed.
  - The next node is pointing to the node that holds the number 1.
- The second node is the `Integer` 1.
  - The actual data this node holds is the number 1.
  - The previous node is the node that holds the number 0.
  - The next node is `null`, indicating that it is the last node in the queue
    and there is no node after it. So when we add a number to the queue, it
    will be added after this node.

It should be noted that each node is stores only the pointer or the link to the
previous and next nodes - not the previous or next nodes' values.

Now let's look at what happens when we add a node:

![LinkedList-Add](https://curriculum-content.s3.amazonaws.com/java-mod-2/queue/LinkedList-Full.png)

- The first node in the queue is still the `Integer` 0.
  - No change has occurred to this node when we add a new node.
- The second node is the `Integer` 1.
  - The actual data this node holds is still the number 1 and has remained
      unchanged.
  - The previous node is the node that holds the number 0 still.
  - The next node is now the node that holds the number 2. It is no longer
      `null` since it is not the last node in the queue anymore so the next
      pointer has been updated with the new addition.
- The third node is the `Integer` 2.
  - The actual data this node holds is the number 2.
  - The previous node is the node that holds the number 1.
  - The next node is `null`, indicating that it is now the last node.

In the above code, we are also removing the nodes. So let's see what happens
when we remove a node for the first time:

![LinkedList-Remove](https://curriculum-content.s3.amazonaws.com/java-mod-2/queue/LinkedList-Remove.png)

Notice that the node that held the number 0 has been removed!

- The first node in the queue is now the `Integer` 1.
  - The actual data this node holds is the number 1 still.
  - The previous node has now changed since we have removed the node that held
      the number 0. Since its previous node was removed and there was no other
      node before the removed node, the new previous node points to `null`
      indicating it is now in the front of the queue.
  - The next node is still the node that holds the number 2 and has remained
      unchanged.
- The second node is the `Integer` 2.
  - The actual data this node holds is still the number 2.
  - The previous node is the node that holds the number 1 still.
  - The next node is still pointing at `null`, indicating it is the last node.

As we go through the queue and call `remove()` repeatedly, we continue to reduce
the size of the queue until it is eventually empty, at which point the
`myNumbers.isEmpty()` call returns `false` and the `while` loop ends.

## Commonly Used Methods

Here are the key methods specific to the `Queue` interface:

| Method                 | Return Type                      | Description                                                         |
|------------------------|----------------------------------|---------------------------------------------------------------------|
| `add(Element item)`    | boolean                          | Adds an item to the end of the queue                                |
| `remove(Element item)` | element that is removed          | Removes an item from the beginning of the queue                     |
| `element()`            | element at the head of the queue | Gets the item at the beginning of the queue, but does not remove it |

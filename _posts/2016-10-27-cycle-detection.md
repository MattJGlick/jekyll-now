---
layout: post
title: HackerRank - Cycle Detection
---
Been awhile since I've dealt with some linked lists so figured I would work through a cycle detection problem. I picked this one [here](https://www.hackerrank.com/challenges/detect-whether-a-linked-list-contains-a-cycle) from HackerRank. 

The basic idea is that you have a linked list and you need to determine if any loops exist in the list. The picture here outlines it quite well.

<p align="center">
  <img src="https://s3.amazonaws.com/hr-challenge-images/1163/1463778594-900a0ae522-inputs.png">
</p>

The first one is just a single node list, so obviously no cycle exits, where the second one has a cycle from 3->2

## Realizations:
The first thing that jumps to mind is that I can store each of the nodes in a list and then see if that node ever reappears. If it doesn't reappear, then you don't have a cycle. If it does, then you do.

The better solution uses a specific algorithm called the "tortoise and the hare" which doesn't require any more data structures. I'm going to use python this time just to mix it up, I'll do the list way first then handle the optimal solution

## Storing Nodes as Python List

Simple traversal, just go through the linked list and check to see if the node exists in the seenNodes. If it's not in the seenNodes add it. If we get to the end, then there were no loops.

```
def has_cycle(head):
    seenNodes = []
    
    cur = head
    while cur.next:
        cur = cur.next
        
        if cur in seenNodes:
            return 1
        else:
            seenNodes.append(cur)          
            
    return 0
```


### Anaylsis

*Runtime*: O(n)

*Space*: O(n)

As we increase the size of the linked list the time it will take to go through the entire linked list will increase. Also, since we have a data structure for storing the seen nodes, our space complexity will increase as our linked list gets bigger.

## "Tortoise and the Hare" 

The "Tortoise and the Hare" algorithm involves two different pointers that travel the linked list at two different speeds. If at any point either of the pointers are pointing at the same node, we know we have a cycle.

```
def has_cycle(head):
    tortoise = head
    hare = head
    
    while hare and hare.next:
        tortoise = head.next
        hare = head.next.next
        
        if tortoise == hare:
            return 1
        
    return 0
```

The hare pointer is twice as fast as the tortoise and therefore will always be ahead of him. The hare will find a cycle before the tortoise and therefore at some point in the future the hare and tortoise will both find their way into the cycle. Once in the cycle they will eventually find each other.

### Anaylsis

*Runtime*: O(n)

*Space*: O(1)

While we still need to traverse through the linked list looking for the cycle, we don't need to store any other data structures. So our while our runtime is determined based on the size of the linked list, the space will never need to be increased.

## Thoughts

Overall I think the list is the more intuitive solution, but the "Tortoise and the Hare" algorithm is the better option. Overall good problem working with linked list and usage of memory.


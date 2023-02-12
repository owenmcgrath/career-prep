# Linked List
- Singly linked lists each node points to the next node.
- Doubly linked lists each node points to a previous node and a next node
- Insertion is O(n) time
- Adding to the front or back is O(1) time
## Creating a Linked List
- its important to specify/ask whether a data structure is singly or doubly linked list
- Nodes hold references to either Prev, next or both nodes
## Deleting from a linked list
- Simply changing the reference from next to next.next or prev to prev.prev
- You may have to do memory cleanup w/ free (c or c++)
## The runner technique
- 2 pointers where one moves faster than the other. "weave" example
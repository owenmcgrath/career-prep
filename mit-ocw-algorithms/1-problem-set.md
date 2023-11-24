# 1-2
[16 points] Given a data structure D that supports Sequence operations:
• D.build(X) in O(n) time, and
• D.insert at(i, x) and D.delete at(i), each in O(log n) time,
where n is the number of items stored in D at the time of the operation, describe algorithms to
implement the following higher-level operations in terms of the provided lower-level operations.
Each operation below should run in O(k log n) time. Recall, delete at returns the deleted item.
(a) reverse(D, i, k): Reverse in D the order of the k items starting at index i (up to
index i + k − 1).
(b) move(D, i, k, j): Move the k items in D starting at index i, in order, to be in front
of the item at index j. Assume that expression i ≤ j < i + k is false. 

## attempt
(a) 
first check if i < n AND i + k - 1 < N
two variables high = i+ k -1, low = i 
while high > low
    toTheFront = D.delete_at(high)
    toTheBack = D.delete_at(low)
    D.insert_at(low, toTheFront)
    D.insert_at(high, toTheBack)
    high--, low++

(b)
j is never between i and i+k. 
but it could be before or after. 

for each k.
    valToMove = d.delete_at(i)
    d.insert_at(j+1, valToMove) 

# 1-3

Sisa Limpson is a very organized second grade student who keeps all of her course notes on individual pages stored in a three-ring binder. If she has n pages of notes in her binder, the first page
is at index 0 and the last page is at index n − 1. While studying, Sisa often reorders pages of her
notes. To help her reorganize, she has two bookmarks, A and B, which help her keep track of
locations in the binder.
Describe a database to keep track of pages in Sisa’s binder, supporting the following operations,
where n is the number of pages in the binder at the time of the operation. Assume that both
bookmarks will be placed in the binder before any shift or move operation can occur, and that
bookmark A will always be at a lower index than B. For each operation, state whether your
running time is worst-case or amortized.

| function         |           description | 
| ---------------  | --------------------- |
| build(X)         | Initialize database with pages from iterator X in O(|X|) time. |
| place mark(i, m) | Place bookmark m ∈ {A, B} between the page at index i and the page at index i + 1 in O(n) time. |
| read page(i)     | Return the page at index i in O(1) time. |
| shift mark(m, d) | Take the bookmark m ∈ {A, B}, currently in front of the page at index i, and move it in front of the page at index i + d for d ∈ {−1, 1} in O(1) time. |
| move page(m)     | Take the page currently in front of bookmark m ∈ {A, B}, and move it in front of the other bookmark in O(1) time. |

A page can be a bookmark that can be inserted. Since there are two bookmarks, the database should be a sequence interface of length n+2.  

build(x)
clear any existing pages and initialize a new array of length x
while iterating x
    add the new page from the iterator

this is worst case runtime O(n)

place_mark(i, m)

store a variable a_idx and b_idx associated with the bookmark on the front of page i
This is worst case runtime O(1)

read_page(i)
    return page[i]

This is worst case runtime O(1)

shift_mark(m,d)
    newIdx = m_idx + d
    if the new index is out of range 0 pagelength - 1
    else m_idx = new_idx

move_page(m)
    if m_idx == 0 return can't do
    idk...

# 1-4
Problem 1-4. [44 points] Doubly Linked List
In Lecture 2, we described a singly linked list. In this problem, you will implement a doubly
linked list, supporting some additional constant-time operations. Each node x of a doubly linked
list maintains an x.prev pointer to the node preceeding it in the sequence, in addition to an
x.next pointer to the node following it in the sequence. A doubly linked list L maintains a pointer
to L.tail, the last node in the sequence, in addition to L.head, the first node in the sequence.
For this problem, doubly linked lists should not maintain their length.
(a) [8 points] Given a doubly linked list as described above, describe algorithms to implement the following sequence operations, each in O(1) time.
insert first(x) insert last(x) delete first() delete last()
(b) [5 points] Given two nodes x1 and x2 from a doubly linked list L, where x1 occurs
before x2, describe a constant-time algorithm to remove all nodes from x1 to x2 inclusive from L, and return them as a new doubly linked list.
(c) [6 points] Given node x from a doubly linked list L1 and second doubly linked list L2,
describe a constant-time algorithm to splice list L2 into list L1 after node x. After the
splice operation, L1 should contain all items previously in either list, and L2 should
be empty.
(d) [25 points] Implement the operations above in the Doubly Linked List Seq
class in the provided code template; do not modify the Doubly Linked List Node
class. You can download the code template including some test cases from the website. 

(a)
insert_first(x)
    if L.head not null:
        x.next = L.head
        L.head.prev = x
    else 
        L.tail = x
    L.head = x

insert_last(x)
    if tail not null:
        tail.next = x
        x.prev = L.tail
    else
        L.head = x
    L.tail = x

delete_first()
    if L.head not null and L.head.next not null
        L.head.next.prev = null
        L.head = L.head.next
    else 
        L.head = null
        L.tail = null

delete_last()
    if L.tail not null and L.tail.prev not null
        L.tail.prev.next = null
        L.tail = L.tail.prev
    else
        L.head = null
        L.tail = null

(b)
remove_from_x1_to_x2(x1,x2)
    if x1 is L.head
        L.head = x2.next
        L.head.prev = null
    else
        temp = x2.next
        x2.next.prev = x1.prev
        x1.prev.next = temp
        

(c)

//assume x is not null
splice(x, L1, L2)
    if x is L1.tail
        L1.tail = L2.tail
    temp = x.next
    x.next = L2.head
    L2.head.prev = x
    L2.tail.next = temp
    temp.prev = L2.tail
    L2.head = null
    L2.tail = null

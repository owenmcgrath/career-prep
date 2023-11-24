# Problem Session 1
## 1-1
a. f5 f3 f2 f1  f4
O((log n)^a) < O(n^b) for any positive a and b

d.  f3 f1 f2  f4 f1

N! sterlings approximation > sqrt(2 * pi * n) * (n/e) ^ n

# 1-2
a. 

front = delete_first
back = delete_last
insert_first(back)
insert_last(front)

all in O(1) time. 

b. 

I guess the question is can you use space? If so its pretty easy to treat the second d like a stack
I am certainly overthinking this. the kth item will be last

loop from 1 to k
D.insert_last(D.delete_first);

# 1-3

essentially just need to hold a reference to the end and the beginning.

insert_front put it in front. if this is the first value, set the last to be this. 
insert_end put it next to last. set this to last.


# 1-4

to reverse a linked list
have two variables 
head 
headnext
fast

also have an iterator thats goes twice trying to find the head everytime.

if theres either 0 or 1 kids return L.

loop fast twice 
temp is headnext.next
headnext->next = head
head = temp

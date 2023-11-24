# Data Structure and Dynamic Arrays.
- Interface vs Data Structure
- Interface is the specification and what data can store
  - what data can store, what operations are supported, what they mean
- Data structure is representation and how to store the data

## 2 main interfaces
- set
- sequence

## 2 main DS approaches
- arrays
- pointer based

## static sequence interface
n items x0, x1, x2 ... xn-1
build() makes a new Datastructure
    for items in x
len() returns n
iter_seq() output x0, x1, xn-1 in sequence order
get_at(i) return xi
set_sat(i,x) set xi to x

Solution(natural): static array.
Key: word ram model of computation
    memory = array of w-bit words
Array: Consecutive Chunk of memory. 
array[i] = memory[address(array) + i]
array access is constant time
O(1): get_at and set_at, len
O(n): build/iter_seq

Memory allocation model: allocate array of size in in O(n) time.
space -> O(time)

assume W (wordsize) >= log(n)

## Dynamic sequence interface.
-insert_at(i,x) make x the new xi, shifting existingxi ... xn-1 over 1
-delete_at(i,x) shift xi+1...x(n-1) to the left 1

static arrays take O(n) time for insert and delete, even at the front and back. because at the back you have to reallocate the memory

linked list insert and delete first are O(1) time. 
get_at and set_at take a long time though! O(n).


## Linked List
Store items in nodes

\[x0| \] -> \[x1 | \] -> \[x2 | \]

gives you the ability to easily reorder, insert, and delete compared to the static array

## Dynamic Arrays
lists in python, vector in c++.
- relax constraint that the size of the array = n, # items in sequence
- enforce size of the array is O(n)
- maintain A\[i\] = xi

length: number of elements
size: the amount of memory.

What if you try to insert when n = size ?
if n = size:
    allocate new array of 2 * size 

so insert_last from empty array resizes at n = 1,2,4,8,16....
resize costs O(sigma from i=0 to logn 2^i) -> O(2^log(n)) = O(n)
kind of O(n)! this is amortization:
    operation takes T(n) amortized time if any k operations take <= k*T(n)

# 1-2
This sounds like binary search! but you can't binary search because theres infinite planets

1. visit planet 2^m from m=0 until k <= 2^m
2. then binary search from m-1 to m

# 1-3

set as a sorted array
and a doubly linked list to store the order

combine to create a map with key as the unique id and the linked list node as the value

1. initialize an object with an empty vector
2. using a stored counter, place that counter value on the back of the vector and iterate the counter
3. reverse the image array and return  it
4. either incrementally move x to the right or the left depending on its relative location to x

# Arrays and strings
- Be aware array & string questions are very often interchangeable

## Hash Tables
- Hash tables are an array structure with O(1) lookups
- Example with array of linked lists and a hash code function
    1. First get hash code (int or long). Different keys might have the same hash code!
    2. Map the hash code to an index in the array. Could be done with hash(key) % length. (not guaranteed unique)
    3. At this index there is a linked list for the key-value pair. This is done to handle the collisions (matching indices)
- To access, generate the hash code for the request, check if that key exists in the linked list.
- In the simple implementation, when the number of collisions is high worst case is O(n)
- In a good implementation, lookup is O(1)
- A different lookup system would use a balanced BST, with O(log(n)) lookup time. This saves space!

## Array List & Resizable Arrays
- Arrays are fixed allocated, Array Lists dynamically change their size. Both still provide O(1) access. 
- When the initial allocation fill up, resizing usually doubles in size. This is a rare case. Insertion is generally O(1), but could be O(n)
- Suppose array of size N, work backwards to determine number of copies at each capacity increase. 
  - When increasing array to K elements, last copy is n/2, prev is n/4, prev is n/8 .... 2, then 1
  - This is always smaller than O(n). Most insertions are O(1), some are O(n)

## StringBuilder
- If you concatenated a list of strings, what would be the runtime?
  - Each string (n strings) copies x characters. 
  - On each iteration a copy of the string is made that copies x characters
  - x char copy -> 2x char copy -> 3x char copy .... 
  - Arithmetic sum formula, n(n+1)/2 -> n^2 so this is O(xn^2)
- Stringbuilder fixes this problem, as it uses a resizable array
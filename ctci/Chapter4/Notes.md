# 4 Trees & Graphs
## Types of Trees
- A tree is a data structure composed of nodes. 
- Each tree has a root node
- The root node has 0 to many child nodes 
- Each child node has 0 to many child nodes and so on.
  
## Tree vs Binary Tree
- A binary tree is when there are two children. Not all trees are binary trees
- a node is called a leaf node when it has no children
  
## Binary Tree vs Binary Search Tree.
- A binary search tree is an ordered from left to right binary tree.
- Some BST can have duplicate values, others put duplicates to the right

## Balanced vs unbalanced
- Balanced means that the tree is wide enough to ensure O(log n) time. Unbalanced would mean more like O(n)
- Complete binary tree: every level other than the last level is filled
- Full Binary Tree: every node has 0 or two children
- Perfect binary tree. All levels are filled.

## Traversal
- In-Order traversal, see every node left to right. Visits in ascending order in BST
```
InOrderTraverse(Node n)
{
    if(n != null)
    {
        InOrderTraversal(n.left);
        visit(n);
        InOrderTraversal(n.right);
    }
}
```
- Preorder traversal, visits current node before child nodes. Root is always first node visited
```
PreOrderTraverse(Node n)
{
    if(n != null)
    {
        visit(n);
        InOrderTraversal(n.left);
        InOrderTraversal(n.right);
    }
}
```
- Postorder traversal, visits children before current node. Root is last node visited
```
PostOrderTraverse(Node n)
{
    if(n != null)
    {
        InOrderTraversal(n.left);
        InOrderTraversal(n.right);
        visit(n);
    }
}
```

## Binary Heaps (min/max heaps)
- max heaps - descending. Min heaps ascending
- a min heap is a complete binary tree where each node is smaller than its children.
- two operations. ExtractMin and Insert
- insert: insert element at the bottom, then swap the value up to the root until its the smallest value. O(log n) time.
- ExtractMin. Getting the value is easy. Removing it is hard. 
- Place the bottom most element with the root, then bubble it down so its the bottom. This takes O(log n) time. 

## Tries
- Sometimes called a prefix tree.
- The * node or null node indicates a complete word. i.e. M - A - N - Y - *
- A node in a trie could have 1 to alphabet size + 1 children. 
- Used to store entire english language for prefix lookups. Can check if its a valid prefix in O(k) time.

## Graphs
- A tree is a graph but not all graphs are trees.
- A graph is collection of nodes with edges between them. 
  - Can be directed (1 way) or undirected (2 way).
  - If theres a path between all vertices its a "connected" graph.
  - Acyclic graph is a graph without cycles.

### Adjacency list
- Most common. Every vertex stores a list of adjacent vertices
- Can be stored as a tree structure. 
- An array or hash table of lists can be used to represent adjacency instead of a tree, probably won't be as clean though.

### Adjacency Matrix
- nxn boolean matrix where "true" at i, j means that nodes i and j are connected.
- finding neighbors is less efficient, since you need to iterate through the whole matrix.

## Graph Search
- DFS and BFS.
- DFS search through the entire branch before going to another branch.
- BFS explore each neighbor before going deep.
- DFS is better for traversing every node in the graph.
- BFS is better for finding the shortest path 

### DFS
```
void search(Node root)
{
    if(root == null) return;
    visit(root);
    root.visited = true;
    for each Node n in root.adjacent:
        if !n.visited:
            search(n)
}
```
- tree traversals are a form of DFS. must note if the node has been visited.
### BFS
- Not recursive, uses a queue.
```
void search(Node root)
{
    Queue q = new Queue();
    root.marked = true;
    queue.enqueue(root);

    while(!queue.IsEmpty())
    {
        Node r = q.dequeue();
        visit(r);
        foreach(Node n in r.adjacent)
        {
            if(n.marked == false)
            {
                n.marked = true;
                queue.enqueue(n);
            }
        }
    }
}
```

### Bidirectional search.
- Finds the shortest path between source and destination node
- Runs two simultaneous BFS searches one from each node. 
- This runs in k^n/2 vs k^n time of a single BFS. 

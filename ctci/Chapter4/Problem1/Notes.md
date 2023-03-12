# Problem 4.1
## Problem statement
Route Between Nodes: Given a directed graph and two nodes (S and E) design and algorithm to find out whether there is a route from S to E. 

## Solution Attempt

### Listen
Directed: No bidirectional search here so need to use a BFS. 
How are the nodes defined? boolean for visited, list of nodes for adjacent.

## Examples
s - c, s - b, b-e. returns true, path found
s - c, s - b, e - s returns false, no path found

## Brute Force

We could just do a DFS through all the nodes of S. i.e recursively looking through the child nodes and marking that we have visited that node. 

## Optimize

Traversing through a graph is always going to be O(m+n) nodes + edges count. 

The best way to typically do path generating between two nodes in a graph is breadth first search. This is because depth first 
search will force us to traverse nodes extra nodes we don't need at a depth beyond where are target is, breadth first won't explore greater depths. Staying closer to the root will mean we will find the shorter path to the root as well. 

But BFS uses O(m) memory as well as it will pop things onto the queue.
Do we expect to ingest big graphs? Maybe memory is a concern here. If we expect to ingest small graphs i recommend BFS. 
If not lets to DFS.

## Walk Through

Initialize a queue. 
mark s as visited.
add s to the queue. 
while the q isnt empty
    pop the queue. as "parent"
    loop through the adjacency list of the parent. as "child"
        if the child is e, return true.
        if the child hasnt been visited
            mark the child as being visited,
            pop it onto the queue.
        
return false. We've looped through the array.

## Implement

'''
public class TreeNode
{
    public bool visited;

    public List<TreeNode> adjacent;

    public TreeNode()
    {
        adjacent = new List<TreeNode>();
    }
}

bool RouteBetweenNodes(TreeNode s, TreeNode e)
{
    if(s == null || e == null) return false;

    Queue<TreeNode> q = new Queue<TreeNode>();
    s.visited = true;
    q.Enqueue(s);

    while(q.Count > 0)
    {
        TreeNode parent = q.Dequeue();
        foreach(TreeNode child in parent.adjacent)
        {
            if(child == e) return true;
            if(!child.visited)
            {
                child.visited = true;
                q.Enqueue(child);
            }
        }
    }

    return false;
}
'''

## Test
s - c, s - b, b-e. returns true, path found
push s on the queue.
c is not e and hasnt been visited, on the queue.
b is not e and hasnt been visited, on the queue. 
c has no children
e is the answer, return true there is a path.

s - c, s - b, e - s returns false, no path found
push s on the queue
c is not e and hasnt been visited, on the queue
b is not e and hasnt been visited, on the queue.
c has no children
b has no children
return false.

null test
We arent handling null s and e. 

## Notes. 
had to google runtimes for bfs and dfs
didnt ask for null handling.
didnt use DFS as the brute force, which i should have.
assume visited is false.
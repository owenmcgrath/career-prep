# Problem 4.7

## Problem statement

You are given a list of projects and a list of dependencies (which is a list of pairs of projects where the second project is dependent on the first project). All of the projects dependencies must be built before the project is. Find a build order that will allow the projects to be built. If there is no valid build order, return an error.

## Solution Attempt

### Listen

What data types for each of the inputs? List of characters for projects. List of Pairs of characters for the dependencies.
Can dependencies be circular? Yes, that would be an invalid build.
Can i assume the characters in the list of projects are unique. (no matching projects) yes.
Can I edit the list of projects in place? Yes.
Can I accept the list of projects as a hash set into the function? yes.

## Examples

## Brute Force
We should create a graph data structure from the dependency pair list where each has an adjacency list of parents, and an 
adjacency list of children. The parents are the dependency for that item. The children are all other nodes that have a dependency
on this node. 

We should store the nodes in a hashtable (since we can assume that the character identifiers of the project are unique)
First we generate the tree and assign each instantiated node into the hashtable.
Then we can iterate through the project list, accessing the root of each parent, then recursively building each of the children for that root.
Building meaning just appending to the list, removing from the hashtable as we build. 

If we encounter the value as anothers parent dependency we can skip it as its already been built, removing it from that tree

## Optimize

We could make this O(m + n) space by making all adjacency lists arrays of characters. It becomes much more complicated if we do that.
I recommend making the adjacency lists hashtables for ease of removal and insertion. This makes space O(m*n)

We are looking at O(m + n) runtime, that includes building the graph and traversing it. 

We dont need to remove from the tree if we use the copied hashset. 

We also don't need a dependent adjacent list. that cleans up the amount of hashsets we need to use. 

We don't really need to use a hashset for the adjacency list either, we never really need to destroy the tree so we can always loop. 

Since we get to define the graph node, we don't need a hashset either. We can mark a project as "visited"

## Walk Through

loop through the dependencies. if the hashset doesn't contain the First, initialize a new node for that
otherwise grab from the hashset. 
set the child adjacency list on that node to include the second. 

iterate through the hashset 
    for each project node, recurse to a node where theres no dependencies.
        mark the node as visited and append it to the list., then return


## Implement

'''
class ProjectNode
{
    char project;
    bool built;
    List<ProjectNode> dependencies;

    ProjectNode()
    {
        dependencies = new List<ProjectNode>();
    }
}

Dictionary<char, ProjectNode> GenerateBuildOrderGraph(List<char> projects, List<Pair<char,char>> dependencies)
{
    Dictionary<char, ProjectNode> graph = new Dictionary<char, ProjectNode>();
    foreach(Pair<char,char> dependency in dependencies)
    {
        ProjectNode nodeToAdd;
        if(!graph.ContainsKey(dependency.First))
        {
            nodeToAdd = new ProjectNode();
            nodeToAdd.projcet = dependency.First;
        }
        else 
        {
            nodeToAdd = graph[dependency.First];
        }
        nodeToAdd.dependencies.Add(dependency.Second);
    }

    return graph;
}

void TraverseBuildOrderGraph(ref List<char> buildOrder, ProjectNode node)
{
    int builtCount = 0;
    foreach(ProjectNode dependency in node.dependencies)
    {
        if(!dependency.built)
        {
            TraverseBuildOrder(buildOrder, dependency);
        }
    }
    buildOrder.Add(node.project);
    node.built = true;
}

List<char> BuildOrder(List<char> projects, List<Pair<char,char>> dependencies)
{
    if(projects == null) return null;
    if(dependencies == null) return projects;
    List<char> buildOrder = new List<char>();
    Dictionary<char, ProjectNode> graph = GenerateBuildOrderGraph(projects, dependencies);
    foreach(ProjectNode pn in graph.Values)
    {
        TraverseBuildOrderGraph(ref buildOrder, pn);
    }

    //for projects that had no dependencies.
    foreach(char project in projects)
    {
        if(!graph[project].built)
        {
            buildOrder.Add(project);
        }
    }

    return buildOrder;
}

'''

## Test


## Notes. 
- Have a pretty clean solution here. 
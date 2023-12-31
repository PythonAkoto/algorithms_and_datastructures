# 133. Clone Graph

Given a reference of a node in a **connected** undirected graph.

Return a **deep copy** (clone) of the graph.

Each node in the graph contains a value (`int`) and a list (`List[Node]`) of its neighbors.

```
class Node {
    public int val;
    public List<Node> neighbors;
}
```

**Test case format:**

For simplicity, each node's value is the same as the node's index (1-indexed). For example, the first node with `val == 1`, the second node with `val == 2`, and so on. The graph is represented in the test case using an adjacency list.

**An adjacency list** is a collection of unordered **lists** used to represent a finite graph. Each list describes the set of neighbors of a node in the graph.

The given node will always be the first node with `val = 1`. You must return the **copy of the given node** as a reference to the cloned graph.


Example 1:

Input: `adjList = [[2,4],[1,3],[2,4],[1,3]]`
Output: `[[2,4],[1,3],[2,4],[1,3]]`
```
Explanation: There are 4 nodes in the graph.
1st node (val = 1)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
2nd node (val = 2)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
3rd node (val = 3)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
4th node (val = 4)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
```

Example 2:

Input: `adjList = [[]]`
Output: `[[]]`
Explanation: Note that the input contains one empty list. The graph consists of only one node with `val = 1` and it does not have any neighbors.

# Python 
```
class Solution:
    def cloneGraph(self, node: "Node") -> "Node":
        # Create a dictionary to map the original nodes to their corresponding new copies.
        oldToNew = {}

        # Depth-first search function to traverse and clone the graph.
        def dfs(node):
            # If the node has already been cloned, return the corresponding new copy.
            if node in oldToNew:
                return oldToNew[node]

            # Create a new node with the same value as the original.
            copy = Node(node.val)

            # Map the original node to its new copy in the dictionary.
            oldToNew[node] = copy

            # Recursively clone the neighbors of the current node.
            for nei in node.neighbors:
                # Append the cloned neighbor to the new node's list of neighbors.
                copy.neighbors.append(dfs(nei))

            # Return the cloned node.
            return copy

        # Start the cloning process from the input node, or return None if the input is None.
        return dfs(node) if node else None
```

# JavaSript
```
var cloneGraph = function(node, seen = new Map()) {
    const isBaseCase = node === null;
    if (isBaseCase) return null;

    if (seen.has(node)) return seen.get(node);

    return dfs(node, seen);                              /* Time O(V + E) | Space O(N) */
}

const dfs = (node, seen) => {
    const clone = new Node(node.val);

    seen.set(node, clone);                               /*               | Space O(N) */

    for (const neighbor of node.neighbors) {
        const cloneNeighbor = cloneGraph(neighbor, seen);/* Time O(V + E) | Space O(H) */

        clone.neighbors.push(cloneNeighbor);             /*               | Space O(V + E) */
    }

    return clone;
}
```
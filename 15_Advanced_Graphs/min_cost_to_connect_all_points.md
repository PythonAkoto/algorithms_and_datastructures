# 1584. Min Cost to Connect All Points
## Compnay: 

You are given an array `points` representing integer coordinates of some points on a 2D-plane, where `points[i] = [xi, yi]`.

The cost of connecting two points `[xi, yi]` and `[xj, yj]` is the **manhattan distance** between them: `|xi - xj| + |yi - yj|`, where `|val|` denotes the absolute value of `val`.

*Return the minimum cost to make all points connected.* All points are connected if there is **exactly one** simple path between any two points.

Example 1:

Input: `points = [[0,0],[2,2],[3,10],[5,2],[7,0]]`
Output: `20`
Explanation: 
We can connect the points to get the minimum cost of 20.
Notice that there is a unique path between every pair of points.

Example 2:

Input: `points = [[3,12],[-2,5],[-4,1]]`
Output: `18`

# Python
```
from typing import List
import heapq

class Solution:
    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        # Number of points
        N = len(points)
        
        # Create an adjacency list to represent the graph
        # adj[i] stores a list of [cost, node] for all nodes connected to node i
        adj = {i: [] for i in range(N)}

        # Populate the adjacency list with distances between points
        for i in range(N):
            x1, y1 = points[i]
            for j in range(i + 1, N):
                x2, y2 = points[j]
                dist = abs(x1 - x2) + abs(y1 - y2)
                adj[i].append([dist, j])
                adj[j].append([dist, i])

        # Prim's algorithm to find minimum spanning tree
        res = 0  # Initialize the result
        visit = set()  # Set to keep track of visited nodes
        minH = [[0, 0]]  # Priority queue to store [cost, point]

        # Continue until all nodes are visited
        while len(visit) < N:
            cost, i = heapq.heappop(minH)  # Get the minimum cost edge
            if i in visit:
                continue  # Skip if the node is already visited
            res += cost  # Add the cost to the result
            visit.add(i)  # Mark the node as visited
            for neiCost, nei in adj[i]:
                if nei not in visit:
                    heapq.heappush(minH, [neiCost, nei])  # Add neighbors to the priority queue

        return res  # Return the total cost of the minimum spanning tree
```

# JavaScript
```
// Function to find the minimum cost to connect points
const minCostConnectPoints = (points) => {
    // Check if it is a base case
    const isBaseCase = ((points.length === 0) || (1000 <= points.length));
    if (isBaseCase) return 0;

    // Build the graph and initialize data structures
    const { graph, seen, minHeap } = buildGraph(points);

    // Search for the minimum cost using Prim's algorithm
    return search(points, graph, seen, minHeap);
};

// Initialize the graph data structures
const initGraph = (points) => ({
    graph: new Array(points.length).fill().map(() => []),
    seen: new Array(points.length).fill(false),
    minHeap: new MinPriorityQueue()
})

// Build the graph with edges and costs
const buildGraph = (points) => {
    const { graph, seen, minHeap } = initGraph(points);

    for (let src = 0; src < (points.length - 1); src++) {
        for (let dst = (src + 1); (dst < points.length); dst++) {
            const cost = getCost(points, src, dst);

            // Add edges and costs to the graph
            graph[src].push([ dst, cost ]);
            graph[dst].push([ src, cost ]);
        }
    }

    // Enqueue the initial node into the priority queue
    const [ src, cost, priority ] = [ 0, 0, 0 ];
    const node = [ src, cost ];
    minHeap.enqueue(node, priority);

    return { graph, seen, minHeap };
}

// Calculate the cost between two points
const getCost = (points, src, dst) => {
    const [ [ x1, y1 ], [ x2, y2 ] ] = [ points[src], points[dst] ];

    return (Math.abs(x1 - x2) + Math.abs(y1 - y2));
}

// Perform the search using Prim's algorithm
const search = (points, graph, seen, minHeap, nodeCount = 0, cost = 0) => {
    while (nodeCount < points.length) {
        let [ src, srcCost ] = minHeap.dequeue().element;

        // Skip if the node is already visited
        if (seen[src]) continue;
        seen[src] = true;

        cost += srcCost;
        nodeCount += 1;

        // Enqueue neighbors into the priority queue
        checkNeighbors(graph, src, seen, minHeap);
    }

    return cost;
}

// Enqueue neighboring nodes into the priority queue
const checkNeighbors = (graph, src, seen, minHeap) => {
    for (const [ dst, dstCost ] of graph[src]) {
        // Skip if the neighbor is already visited
        if (seen[dst]) continue;

        // Enqueue the neighbor into the priority queue
        minHeap.enqueue([ dst, dstCost ], dstCost);
    }
}
```
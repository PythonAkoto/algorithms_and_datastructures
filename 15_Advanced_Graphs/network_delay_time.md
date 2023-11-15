# 743. Network Delay Time
## Company: Google

You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source node, `vi` is the target node, and `wi` is the time it takes for a signal to travel from source to target.

We will send a signal from a given node `k`. Return *the **minimum** time it takes for all the n nodes to receive the signal*. If it is impossible for all the n nodes to receive the signal, return -`1`.


Example 1:


Input: `times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2`
Output: `2`

Example 2:

Input: `times = [[1,2,1]], n = 2, k = 1`
Output: `1`

Example 3:

Input: `times = [[1,2,1]], n = 2, k = 2`
Output: `-1`

# Python
```
from typing import List
import heapq
import collections

class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        # Create a defaultdict to store the edges for each node
        edges = collections.defaultdict(list)
        for u, v, w in times:
            edges[u].append((v, w))

        # Priority queue to store (weight, node) pairs
        minHeap = [(0, k)]
        visit = set()  # Set to keep track of visited nodes
        t = 0  # Variable to store the total time

        # Dijkstra's algorithm to find the minimum time to reach each node
        while minHeap:
            w1, n1 = heapq.heappop(minHeap)

            # Skip if the node is already visited
            if n1 in visit:
                continue

            visit.add(n1)  # Mark the node as visited
            t = w1  # Update the total time

            # Explore neighbors of the current node
            for n2, w2 in edges[n1]:
                if n2 not in visit:
                    # Enqueue the neighbor with updated time into the priority queue
                    heapq.heappush(minHeap, (w1 + w2, n2))

        # Return the total time if all nodes are visited, otherwise return -1
        return t if len(visit) == n else -1

# Time complexity: O(E * log(V))
```
# JavaScript
```
// Function to find the network delay time
var networkDelayTime = (times, n, k) => {
    // Build the graph and initialize data structures
    const { graph, seen, minHeap } = buildGraph(times, n, k);
    const maxTime = getTime(graph, seen, minHeap);

    // Return the maximum time if all nodes are visited, otherwise return -1
    return (seen.size === n)
        ? maxTime
        : -1;
};

// Initialize the graph data structures
var initGraph = (n, k) => ({
    graph: Array.from({ length: n + 1 }).fill().map(() => []),
    seen: new Set(),
    minHeap: new MinPriorityQueue()
})

// Build the graph with edges and costs
var buildGraph = (times, n, k) => {
    const { graph, seen, minHeap } = initGraph(n, k);

    for (const [src, dst, weight] of times) {
        // Add edges and weights to the graph
        graph[src].push([dst, weight]);
    };

    // Enqueue the initial node into the priority queue
    minHeap.enqueue([k, 0], 0);

    return { graph, seen, minHeap };
}

// Perform the search to find the maximum time using Dijkstra's algorithm
const getTime = (graph, seen, minHeap, maxTime = 0) => {
    while (!minHeap.isEmpty()) {
        const [node, cost] = minHeap.dequeue().element;

        // Skip if the node is already visited
        if (seen.has(node)) continue;

        seen.add(node);  // Mark the node as visited
        maxTime = Math.max(maxTime, cost);  // Update the maximum time

        // Enqueue neighbors into the priority queue
        checkNeighbors(graph, node, cost, seen, minHeap);
    }

    return maxTime;
}

// Enqueue neighboring nodes into the priority queue
var checkNeighbors = (graph, src, srcCost, seen, minHeap) => {
    for (const [dst, dstCost] of graph[src]) {
        // Skip if the neighbor is already visited
        if (seen.has(dst)) continue;

        const cost = dstCost + srcCost;
        const node = [dst, cost];

        // Enqueue the neighbor into the priority queue
        minHeap.enqueue(node, cost);
    }
}
```
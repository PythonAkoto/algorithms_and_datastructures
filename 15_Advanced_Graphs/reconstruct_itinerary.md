# 332. Reconstruct Itinerary
## Company: Google

You are given a list of airline `tickets` where `tickets[i] = [fromi, toi]` represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from `"JFK"`, thus, the itinerary must begin with `"JFK"`. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

- For example, the itinerary `["JFK", "LGA"]` has a smaller lexical order than `["JFK", "LGB"]`.

You may assume all tickets form at least one valid itinerary. You must use all the tickets once and only once.

 

Example 1:

Input: `tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]`
Output: `["JFK","MUC","LHR","SFO","SJC"]`

Example 2:

Input: `tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]`
Output: `["JFK","ATL","JFK","SFO","ATL","SFO"]`
Explanation: Another possible reconstruction is `["JFK","SFO","ATL","JFK","ATL","SFO"]` but it is larger in lexical order.

# Python
```
from typing import List  # Importing List for type hinting

class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        # Creating an adjacency dictionary to store destinations for each source
        adj = {src: [] for src, dst in tickets}
        res = []  # Initialize the result list

        # Populating the adjacency dictionary with destinations for each source
        for src, dst in tickets:
            adj[src].append(dst)

        # Sorting the destinations in lexicographical order
        for key in adj:
            adj[key].sort()

        # Depth-First Search (DFS) function to find the itinerary
        def dfs(adj, result, src):
            if src in adj:  # If the source exists in the adjacency dictionary
                destinations = adj[src][:]  # Copy the destinations for the current source
                while destinations:  # While there are destinations available
                    dest = destinations[0]  # Get the first destination
                    adj[src].pop(0)  # Remove the visited destination
                    dfs(adj, res, dest)  # Recursively visit the next destination
                    destinations = adj[src][:]  # Update the destinations for the source
            res.append(src)  # Append the source after visiting all its destinations

        # Start DFS from "JFK" as the source
        dfs(adj, res, "JFK")
        res.reverse()  # Reverse the itinerary as the DFS appends in reverse order

        # If the itinerary length is not equal to the number of tickets + 1, return an empty list
        if len(res) != len(tickets) + 1:
            return []

        return res  # Return the found valid itinerary
```

# JavaScript
```
var findItinerary = (tickets) => {
    tickets.sort(); // Sort the tickets lexicographically to process them in order

    const graph = buildGraph(tickets); // Build a graph from the given tickets

    return dfs(tickets, graph); // Perform DFS to find the itinerary
};

// Depth-First Search to find the valid itinerary
const dfs = (tickets, graph, city = 'JFK', path = ['JFK']) => {
    const isBaseCase = (path.length === (tickets.length + 1)); // Check if it's the final valid itinerary
    if (isBaseCase) return true; // If the path length is as expected, return true (indicating a valid itinerary)

    const queue = (graph.get(city) || []); // Retrieve destinations for the current city

    const isEmpty = (queue.length === 0); // Check if there are no available destinations
    if (isEmpty) return false; // If there are no destinations, it's not a valid path

    for (const nextCity of queue.slice()) { // Iterate through the available destinations
        path.push(nextCity); // Add the next city to the path
        queue.shift(); // Remove the next city from the available destinations

        if (dfs(tickets, graph, nextCity, path)) return path; // Recursively explore the next city

        path.pop(); // If the path is invalid, remove the last city from the path
        queue.push(nextCity); // Revert the changes in the queue
    }

    return false; // If no valid path is found, return false
};

// Build a graph from the given tickets
const buildGraph = (tickets, graph = new Map()) => {
    for (const [src, dst] of tickets) {
        const edges = (graph.get(src) || []); // Retrieve existing destinations or initialize an empty array

        edges.push(dst); // Add the destination to the edges array
        graph.set(src, edges); // Update the graph with the edges
    }

    return graph; // Return the constructed graph
}
```
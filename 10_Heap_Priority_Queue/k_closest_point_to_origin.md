# 973. K Closest Point to Origin
### Company: Meta

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane and an integer k, return the k closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance `(i.e., √(x1 - x2)2 + (y1 - y2)2)`.

You may return the answer in **any order**. The answer is **guaranteed** to be **unique** (except for the order that it is in).

 

Example 1:


Input: `points = [[1,3],[-2,2]], k = `1
Output: `[[-2,2]]`
Explanation:
```
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].
```

Example 2:

Input: `points = [[3,3],[5,-1],[-2,4]], k = 2`
Output: `[[3,3],[-2,4]]`

Explanation: The answer `[[-2,4],[3,3]`] would also be accepted.

# Python 
```
import heapq  # Import the heapq module for min-heap operations

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]:
        # Create an empty list to store tuples (distance, x, y)
        minHeap = []
        
        # Calculate the squared distance for each point and add it to the minHeap
        for x, y in points:
            dist = (x ** 2) + (y ** 2)  # Calculate the squared Euclidean distance
            minHeap.append((dist, x, y))  # Add the tuple (distance, x, y) to the minHeap
        
        # Convert the list of tuples into a min-heap
        heapq.heapify(minHeap)
        
        # Create an empty list to store the k closest points
        res = []
        
        # Pop the top k points from the minHeap and add them to the result list
        for _ in range(k):
            _, x, y = heapq.heappop(minHeap)  # Extract the point with the smallest distance
            res.append((x, y))  # Add the point (x, y) to the result list
        
        return res  # Return the list of k closest points
```

# JavaScript
```
// Define a function kClosest that takes an array of points and an integer k as parameters.
var kClosest = function (points, k) {
    // Create a MaxPriorityQueue to store the k closest points.
    let maxPQ = new MaxPriorityQueue();

    // Iterate through each point in the input array.
    for (let point of points) {
        // Calculate the squared distance of the current point from the origin.
        let dist = squaredDistance(point);

        // If the max priority queue has fewer than k points, add the current point.
        if (maxPQ.size() < k) {
            maxPQ.enqueue(point, dist); // Add the point with its distance to the max priority queue.
        } 
        // If the max priority queue is full and a closer point is found, replace the farthest point.
        else if (dist < maxPQ.front().priority) {
            maxPQ.dequeue(); // Remove the point with the maximum distance.
            maxPQ.enqueue(point, dist); // Add the current point with its distance.
        }
    }

    // Return an array containing all the points stored in the max priority queue.
    return maxPQ.toArray().map((el) => el.element);
};

// Function to calculate the squared distance of a point from the origin.
function squaredDistance(point) {
    return point[0] * point[0] + point[1] * point[1];
}
```
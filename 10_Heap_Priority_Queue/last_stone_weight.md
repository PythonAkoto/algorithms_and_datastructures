# 1046. Last Stone Weight
### Company: Google

You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

We are playing a game with the stones. On each turn, we choose the **heaviest two stones** and smash them together. Suppose the heaviest two stones have weights `x` and `y` with `x <= y`. The result of this smash is:

- If `x == y`, both stones are destroyed, and
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight y has new weight `y - x`.
At the end of the game, there is at most one stone left.

Return the weight of the last remaining stone. If there are no stones left, return 0.

 

Example 1:

Input: `stones = [2,7,4,1,8,1]`
Output: `1`

Explanation: 
```
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of the last stone.
```

Example 2:

Input: `stones = [1]`
Output: `1`

# Python
```
import heapq
from typing import List

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        # Convert the list of stones into a max-heap by negating the values.
        stones = [-s for s in stones]
        heapq.heapify(stones)

        # Continue smashing stones until there is either one stone left or none.
        while len(stones) > 1:
            # Extract the two largest stones from the max-heap.
            first = heapq.heappop(stones)
            second = heapq.heappop(stones)

            # Calculate the difference between the two stones (destructive impact).
            if second > first:
                heapq.heappush(stones, first - second)

        # If there is one stone left, add it to the list with weight 0.
        stones.append(0)

        # Return the absolute value of the final stone's weight as the result.
        return abs(stones[0])
```

# JavaScript
```
/**
 * Time O(N * log(N)) | Space O(N)
 * @param {number[]} stones
 * @return {number}
 */
var lastStoneWeight = function (stones) {
    // Create a max heap to store the stones
    const maxHeap = getMaxHeap(stones)

    // Shrink the max heap until there is only one stone left
    shrink(maxHeap)

    // Check if the max heap is not empty
    return !maxHeap.isEmpty()
        ? maxHeap.front().element // Return the last stone's weight
        : 0 // If the heap is empty, return 0
};

// Function to create a max heap from an array of stones
const getMaxHeap = (stones, maxHeap = new MaxPriorityQueue()) => {
    for (const stone of stones) {
        maxHeap.enqueue(stone) // Add each stone to the max heap
    }

    return maxHeap // Return the max heap
}

// Function to repeatedly shrink the max heap by smashing two largest stones
const shrink = (maxHeap) => {
    while (1 < maxHeap.size()) {
        // Dequeue the two largest stones
        const [ x, y ] = [ maxHeap.dequeue().element, maxHeap.dequeue().element ]
        
        // Calculate the difference between the two stones
        const difference = x - y;

        // Check if the difference is positive (i.e., there's a remaining stone)
        const isPositive = 0 < difference
        if (isPositive) maxHeap.enqueue(difference); // Add the remaining stone back to the max heap
    }
}
```
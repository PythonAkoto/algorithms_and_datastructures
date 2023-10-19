# 703. Kth Largest Element in a Stream
### Company: Amazon

Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:

- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers nums.
- `int add(int val)` Appends the integer val to the stream and returns the element representing the `kth` largest element in the stream.
 

Example 1:

Input
`["KthLargest", "add", "add", "add", "add", "add"]`
`[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]`

Output
`[null, 4, 5, 5, 8, 8]`

Explanation
```
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
```

# Python
```
import heapq
from typing import List

class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        # Initialize the KthLargest object with k and a list of integers (nums).
        # Use a minHeap to keep track of the K largest elements.
        self.minHeap, self.k = nums, k

        # Convert the initial nums list into a min heap.
        heapq.heapify(self.minHeap)

        # If the length of the minHeap is greater than k, 
        # remove the smallest elements until we have only k elements.
        while len(self.minHeap) > k:
            heapq.heappop(self.minHeap)

    def add(self, val: int) -> int:
        # Add the new value (val) to the minHeap.
        heapq.heappush(self.minHeap, val)

        # If the length of the minHeap exceeds k,
        # remove the smallest element, maintaining the k largest elements.
        if len(self.minHeap) > self.k:
            heapq.heappop(self.minHeap)

        # Return the smallest element in the minHeap, which is the kth largest element.
        return self.minHeap[0]
```

# JavaScript
```
/** 
 * https://leetcode.com/problems/kth-largest-element-in-a-stream/
 * Time O(N * (K * log(K))) | Space O(K)
 * Your KthLargest object will be instantiated and called as such:
 * var obj = new KthLargest(k, nums)
 * var param_1 = obj.add(val)
 */
 class KthLargest {
    /**
     * @param {number} k
     * @param {number[]} nums
     * @constructor
     */
    constructor(k, nums) {
        this.k = k
        this.minHeap = new MinPriorityQueue();

        nums.forEach((num) => this.add(num))
    }

    /**
     * @param {number} val
     * @return {number}
     */
    add(val, { minHeap } = this) {
        const isUnderCapacity = minHeap.size() < this.k;
        if (isUnderCapacity) {
            minHeap.enqueue(val);
        
            return this.top();
        }

        const isLarger = this.top() < val;
        if (isLarger) {
            minHeap.dequeue()
            minHeap.enqueue(val);
        }
        
        return this.top();
    }

    top ({ minHeap } = this) {
        return minHeap.front()?.element || 0
    }
}
```
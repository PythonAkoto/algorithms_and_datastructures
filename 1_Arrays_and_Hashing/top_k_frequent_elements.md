# 347. Top K Frequent Elements
## Company: Amazon

Given an integer array `nums` and an integer `k`, return the `k` *most frequent elements*. You may return the answer in any order.

Example 1:

Input: `nums = [1,1,1,2,2,3], k = 2`
Output: `[1,2]`

Example 2:

Input: `nums = [1], k = 1`
Output: `[1]`

# Python
```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # Dictionary to store the count of each number
        count = {}

        # List to store numbers grouped by frequency
        freq = [[] for i in range(len(nums) + 1)]

        # Count the occurrences of each number in the input list
        for n in nums:
            count[n] = 1 + count.get(n, 0)

        # Group numbers by frequency in the 'freq' list
        for n, c in count.items():
            freq[c].append(n)

        # Result list to store the top k frequent numbers
        res = []

        # Iterate through the 'freq' list in reverse order
        for i in range(len(freq) - 1, 0, -1):
            # Iterate through the numbers in the current frequency group
            for n in freq[i]:
                # Append the number to the result list
                res.append(n)
                # Check if the result list has reached the desired length k
                if len(res) == k:
                    return res

        # The function will only reach this point if k is greater than the number of unique elements in the input list
        return res
```

# JavaScript
```
// Function to find the top k frequent elements in an array
var topKFrequent = function(nums, k) {
    // Map to store the frequency count of each element
    const mp = new Map();

    // Array to store elements grouped by their frequency
    const arr = new Array(nums.length + 1).fill(0);

    // Array to store the final result
    const ans = [];

    // Count the frequency of each element and store it in the map
    nums.forEach(el => {
        const val = mp.get(el) || 0;
        mp.set(el, val + 1);
    });

    // Group elements by frequency in the 'arr' array
    for (let [key, value] of mp) {
        const prev = arr[value] || [];
        prev.push(key);
        arr[value] = prev;
    }

    // Reverse the 'arr' array to iterate from highest to lowest frequency
    arr.reverse();

    // Iterate through the 'arr' array and add elements to the result list
    for (let el of arr) {
        if (k < 1) break;
        if (el) {
            for (let el2 of el) {
                ans.push(el2);
                k--;
            }
        }
    }

    // Return the final result
    return ans;
};
```
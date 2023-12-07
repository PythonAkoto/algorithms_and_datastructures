# 153. Find Minimum in Rotated Sorted Array
## Company: Meta

Suppose an array of length `n` sorted in ascending order is **rotated** between `1` and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

- `[4,5,6,7,0,1,2]` if it was rotated `4` times.
- `[0,1,2,4,5,6,7]` if it was rotated `7` times.
Notice that **rotating** an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` of **unique** elements, return the *minimum element of this array*.

You must write an algorithm that runs in `O(log n) time`.

 

Example 1:

Input: `nums = [3,4,5,1,2]`
Output: `1`
Explanation: The original array was `[1,2,3,4,5]` rotated `3` times.

Example 2:

Input: `nums = [4,5,6,7,0,1,2]`
Output: `0`
Explanation: The original array was `[0,1,2,4,5,6,7]` and it was rotated `4` times.

Example 3:

Input: `nums = [11,13,15,17]`
Output: `11`
Explanation: The original array was `[11,13,15,17]` and it was rotated `4` times.

# Python
```
from typing import List

class Solution:
    def findMin(self, nums: List[int]) -> int:
        # Initialize the start and end indices for binary search
        start, end = 0, len(nums) - 1 
        
        # Initialize a variable to store the current minimum value
        curr_min = float("inf")
        
        # Perform binary search until start index is less than end index
        while start < end:
            # Calculate the middle index
            mid = (start + end) // 2
            
            # Update the current minimum value with the minimum of the current minimum and the value at the middle index
            curr_min = min(curr_min, nums[mid])
            
            # If the value at the middle index is greater than the value at the end index, the minimum is on the right
            if nums[mid] > nums[end]:
                start = mid + 1
                
            # If the value at the middle index is less than or equal to the value at the end index, the minimum is on the left
            else:
                end = mid - 1 
        
        # Return the minimum value between the current minimum and the value at the start index
        return min(curr_min, nums[start])
```

# JavaScript
```
var findMin = function (nums) {
    let [left, right] = [0, nums.length - 1];

    while (left < right) {
        const mid = (left + right) >> 1;
        const guess = nums[mid];
        const [leftNum, rightNum] = [nums[left], nums[right]];

        const isTarget = leftNum < rightNum;
        if (isTarget) return leftNum;

        const isTargetGreater = leftNum <= guess;
        if (isTargetGreater) left = mid + 1;

        const isTargetLess = guess < leftNum;
        if (isTargetLess) right = mid;
    }

    return nums[left];
};
```
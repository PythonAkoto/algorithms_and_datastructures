# Jump Game
## Company: Amazon

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` *if you can reach the last index, or `false` otherwise*.

 

Example 1:

Input: `nums = [2,3,1,1,4]`
Output: `true`
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.

Example 2:

Input: `nums = [3,2,1,0,4]`
Output: `false`
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

# Python
```
from typing import List  # Importing List for type hinting

class Solution:
    def canJump(self, nums: List[int]) -> bool:
        goal = len(nums) - 1  # The goal is to reach the last index of the list

        # Iterate backward through the list from the second-to-last element to the first
        for i in range(len(nums) - 2, -1, -1):
            # Check if the current index 'i' plus the maximum jump length from 'i'
            # can reach or surpass the goal (last index)
            if i + nums[i] >= goal:
                goal = i  # If it can reach, update the goal to this index

        return goal == 0  # Return True if the goal is at the start (index 0), indicating it's possible to reach the end from the start
```

# JavaScript
```
// Function to check if it's possible to jump through the array
// right parameter is initialized to the last index of the array by default
var canJump = (nums, right = nums.length - 1) => {
    for (let i = right; 0 <= i; i--) { // Iterate backward from the right end to the beginning of the array
        const isJumpable = right <= (i + nums[i]); // Check if the current index allows a jump to reach the 'right' position
        if (isJumpable) right = i; // If it's jumpable, update the 'right' position
    }

    return right === 0; // Return true if 'right' has reached the start (index 0), indicating it's possible to reach the end from the start
}
```
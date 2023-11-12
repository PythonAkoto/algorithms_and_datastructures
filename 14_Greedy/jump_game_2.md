# Jump Game II
## Company: Google

You are given a **0-indexed array** of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. In other words, if you are at `nums[i]`, you can jump to any `nums[i + j]` where:

- `0 <= j <= nums[i]` and
- `i + j < n`
Return the minimum number of jumps to reach `nums[n - 1]`. The test cases are generated such that you can reach `nums[n - 1]`.

 

Example 1:

Input: `nums = [2,3,1,1,4]`
Output: `2`
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

Example 2:

Input: `nums = [2,3,0,1,4]`
Output: `2`

# Python 
```
from typing import List  # Importing List for type hinting

class Solution:
    def jump(self, nums: List[int]) -> int:
        l, r = 0, 0  # Initialize the left and right pointers
        res = 0  # Initialize the result variable to count the number of jumps
        
        # Loop until the right pointer reaches the end of the array
        while r < (len(nums) - 1):
            maxJump = 0  # Initialize the variable to track the maximum reachable position
            
            # Iterate through the current range to find the maximum jump position
            for i in range(l, r + 1):
                maxJump = max(maxJump, i + nums[i])  # Update the maximum jump position
            
            l = r + 1  # Update the left pointer to the previous 'r + 1' as the new range start
            r = maxJump  # Update the right pointer to the maximum reachable position found
            res += 1  # Increment the count of jumps
        
        return res  # Return the total number of jumps required to reach the end of the array
```

# JavaScript
```
var jump = function(nums) {
    let [ jumps, currentJumpEnd, farthest ] = [ 0, 0, 0]; // Initialize jump count, current jump end, and farthest reachable position
    
    for (let i = 0; i < nums.length - 1; i++) { // Iterate through the array
        farthest = Math.max(farthest, (i + nums[i])); // Calculate the farthest reachable position
        
        const canJump = i === currentJumpEnd; // Check if the current index is the end of the current jump
        if (canJump) { 
            jumps++; // Increment the jump count
            currentJumpEnd = farthest; // Update the current jump's end to the farthest reachable position
        }
    }

    return jumps; // Return the total number of jumps needed to reach the end
}
```
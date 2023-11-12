# 53. Maximum Subarrary
## Company: Amazon

Given an integer array `nums`, find the **subarray** with the largest sum, and return its *sum*.

 

Example 1:

Input: `nums = [-2,1,-3,4,-1,2,1,-5,4]`
Output: `6`
Explanation: The subarray `[4,-1,2,1]` has the largest sum 6.

Example 2:

Input: `nums = [1]`
Output: `1`
Explanation: The subarray `[1]` has the largest sum 1.

Example 3:

Input: `nums = [5,4,-1,7,8]`
Output: `23`
Explanation: The subarray `[5,4,-1,7,8]` has the largest sum 23.

# Python
```
from typing import List  # Importing List for type hinting

class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        res = nums[0]  # Initialize the maximum sum as the first element in the list

        total = 0  # Initialize a variable to keep track of the current total sum
        for n in nums:  # Iterate through the elements in the list
            total += n  # Add the current element to the running total
            res = max(res, total)  # Update the maximum sum seen so far
            
            if total < 0:  # If the current total sum is negative
                total = 0  # Reset the total sum to 0 (as starting a new subarray from the current element might yield a higher sum)
        return res  # Return the maximum sum of any contiguous subarray in the given list
```

# JavaScript
```
var maxSubArray = function(nums) {
    // Initialize runningSum and maxSum with the first element in the array
    let [ runningSum, maxSum ] = [ nums[0], nums[0] ]
    
    // Loop through the array starting from the second element
    for (let i = 1; i < nums.length; i++) {
        const num = nums[i] // Access the current element in the array
        const sum = runningSum + num // Calculate the sum by adding the current number to the running sum
        
        runningSum = Math.max(num, sum) // Update the runningSum to the maximum between the current number and the sum
        
        maxSum = Math.max(maxSum, runningSum) // Update the maxSum with the maximum between current maxSum and the updated runningSum
    }
    
    return maxSum // Return the maximum sum found in any contiguous subarray
};
```
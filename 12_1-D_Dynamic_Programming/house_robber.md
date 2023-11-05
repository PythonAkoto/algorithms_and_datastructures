# 198. House Robber
### Company: Google

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night.**

*Given an integer array `nums` representing the amount of money of each house, return the maximum amount of money you can rob tonight* ***without alerting the police.***

 

Example 1:

Input: `nums = [1,2,3,1]`
Output: `4`
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.

Example 2:

Input: `nums = [2,7,9,3,1]`
Output: `12`

Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.

# Python
```
class Solution:
    def rob(self, nums: List[int]) -> int:
        # Initialize two variables to keep track of the maximum amount robbed
        # rob1 represents the maximum amount if we rob the previous house
        # rob2 represents the maximum amount if we skip the previous house
        rob1, rob2 = 0, 0

        # Iterate through the list of house values
        for n in nums:
            # Calculate the maximum amount if we rob the current house
            # This is the sum of the current house value and the amount we can get from skipping the previous house (rob1)
            # We compare this value with the amount we would get by skipping the current house (rob2)
            temp = max(n + rob1, rob2)
            
            # Update rob1 to store the value of rob2 (the value for the next iteration)
            rob1 = rob2
            
            # Update rob2 to store the maximum amount calculated for the current house
            rob2 = temp
        
        # Return the maximum amount we can rob after iterating through all the houses
        return rob2
```
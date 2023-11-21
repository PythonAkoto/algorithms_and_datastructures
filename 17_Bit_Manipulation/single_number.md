# 136. Single Number
## Company: Amazon

Given a **non-empty** array of integers `nums`, every element appears *twice* except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

 

Example 1:

Input: `nums = [2,2,1]`
Output: `1`

Example 2:

Input: `nums = [4,1,2,1,2]`
Output: `4`

Example 3:

Input: `nums = [1]`
Output: `1`

# Python
```
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        # Initialize the result variable to 0
        res = 0

        # Iterate through the elements in the input list
        for n in nums:
            # Use bitwise XOR (^) to find the non-repeating element
            # XORing a number with itself results in 0, so all repeating elements will cancel out
            # The final result will be the non-repeating element
            res = n ^ res

        # Return the non-repeating element
        return res
```

# JavaScript
```
// Function to find the single non-repeating number in an array using bitwise XOR
var singleNumber = function (nums, xor = 0) {
    // Iterate through the elements in the input array
    for (num of nums) {
        // Use bitwise XOR (^) to find the non-repeating element
        // XORing a number with itself results in 0, so all repeating elements will cancel out
        // The final result will be the non-repeating element
        xor ^= num;
    }

    // Return the non-repeating element
    return xor;
};
```
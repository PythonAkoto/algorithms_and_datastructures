# 238. Product of Array Except Self
## Company: Amazon

Given an integer array `nums`, return *an array* `answer` such that `answer[i]` *is equal to the product of all the elements of `nums` except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

 

Example 1:

Input: `nums = [1,2,3,4]`
Output: `[24,12,8,6]`

Example 2:

Input: `nums = [-1,1,0,-3,3]`
Output: `[0,0,9,0,0]`

# Python
```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        # Initialize a result array with all elements set to 1
        res = [1] * (len(nums))

        # Calculate the prefix products and update the result array
        for i in range(1, len(nums)):
            res[i] = res[i-1] * nums[i-1]

        # Initialize a variable to store the postfix product
        postfix = 1

        # Update the result array with the postfix products
        for i in range(len(nums) - 1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]

        # Return the final result array
        return res
```

# JavaScript
```
// Function to calculate the product of all elements in an array except itself
function productExceptSelf(nums) {
    // Initialize an array to store the final result
    const result = [];
    
    // Initialize a variable to store the prefix product
    let prefix = 1;
    
    // Calculate the prefix products and update the result array
    for (let i = 0; i < nums.length; i++) {
        result[i] = prefix;
        prefix *= nums[i];
    }

    // Initialize a variable to store the postfix product
    let postfix = 1;

    // Calculate the postfix products and update the result array in reverse order
    for (let i = nums.length - 2; i >= 0; i--) {
        postfix *= nums[i + 1];
        result[i] *= postfix;
    }

    // Return the final result array
    return result;
};
```
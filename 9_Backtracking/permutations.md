# 46. Permutations
### Company: Meta & Google

Given an array `nums` of distinct integers, return all the possible *permutations*. You can return the answer in **any order**.

 

Example 1:

Input: `nums = [1,2,3]`
Output: `[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]`

Example 2:

Input: `nums = [0,1]`
Output: `[[0,1],[1,0]]`

Example 3:

Input: `nums = [1]`
Output: `[[1]]`

# Python
```
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []  # Initialize an empty list to store permutations

        # Base case: If there's only one element in the list, return a list containing that element
        if len(nums) == 1:
            return [nums[:]]  # nums[:] is a deep copy to avoid modifying the original list

        # Iterate through the elements in the input list
        for i in range(len(nums)):
            n = nums.pop(0)  # Pop the element at index 0 to consider for the permutation

            # Recursively find permutations for the remaining elements after excluding n
            perms = self.permute(nums)

            # For each permutation, append n to create a new permutation
            for perm in perms:
                perm.append(n)

            # Extend the result list with the new permutations
            res.extend(perms)

            # Restore the original order of nums by appending n back to its original position
            nums.append(n) 
```

# JavaScript
```
```
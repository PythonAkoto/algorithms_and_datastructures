# 78. Subsets
### Company: Meta

Given an integer array `nums` of **unique** elements, return ***all*** possible 
*subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

 

Example 1:

Input: `nums = [1,2,3]`
Output: `[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]`

Example 2:

Input: `nums = [0]`
Output: `[[],[0]]`

# Python
```
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        # hold all the results
        res = []

        # data structure to hold different values
        subset = []

        # i is the list index currently at
        def dfs(i):
            # if index is at the end
            if i >= len(nums):
                # copy subset and add it to results
                res.append(subset.copy())
                return
            # decision to include nums[i]
            subset.append(nums[i])
            dfs(i + 1)  # recursivley search left branch
            # decision NOT to include nums[i]
            # an empty subset will be given
            subset.pop()
            dfs(i + 1)

        dfs(0) # call function at starting index of list
        return res
```

# JavaScript
```
var subsets = (nums) => {
    nums.sort((a, b) => a - b); // Sort the input array in ascending order

    return dfs(nums); // Call the depth-first search function with the sorted array
}

var dfs = (nums, level = 0, set = [], subset = []) => {
    subset.push(set.slice()); // Push a copy of the 'set' array into the 'subset' array

    for (let i = level; i < nums.length; i++) {
        backTrack(nums, i, set, subset); // Call the backtracking function
    }

    return subset; // Return the 'subset' array containing all subsets
}

const backTrack = (nums, i, set, subset) => {
    set.push(nums[i]); // Add the current number at index 'i' to the 'set' array
    dfs(nums, (i + 1), set, subset); // Recursively explore subsets with the updated 'set'
    set.pop(); // Remove the last added element to backtrack
};

```
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
        res = []

        # base case: return a list containing element if only 1 element in list
        if len(nums) == 1:
            return [nums[:]]  # nums[:] is a deep copy

        # iterate through elements in list
        for i in range(len(nums)):
            # pop element at index 0 for permutation
            n = nums.pop(0)
            # find permuations recursively for remaining after excluding n
            perms = self.permute(nums)

            # for each perm, add n to create new perm
            for perm in perms:
                perm.append(n)
            # extend result list with new perm
            res.extend(perms)
            # restore original order of nums by appending n back to its original positoin
            nums.append(n)
        return res
 
```

# JavaScript
```
 var permute = function(nums) {
    return dfs(nums)
}

var dfs = function(nums, permutation = [], permutations = []) {
    const isBaseCase = nums.length === permutation.length
    if (isBaseCase) return permutations.push(permutation.slice())

    for (let i = 0; i < nums.length; i++) {
        if (permutation.includes(nums[i])) continue;

        backTrack(nums, i, permutation, permutations);
     }

    return permutations;
}

const backTrack = (nums, i, permutation, permutations) => {
    permutation.push(nums[i])
        dfs(nums, permutation, permutations)
    permutation.pop()
}
```
# 39. Contains Sum
### Company: Amazon

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the 
frequency
 of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

 

Example 1:

Input: `candidates = [2,3,6,7], target = 7`
Output: `[[2,2,3],[7]]`
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

Example 2:

Input: `candidates = [2,3,5], target = 8`
Output: `[[2,2,2,2],[2,3,3],[3,5]]`

Example 3:

Input: `candidates = [2], target = 1`
Output: `[]`

# Python
```
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []  # List to store the resulting combinations

        def dfs(i, cur, total):
            # The depth-first search function to explore combinations
            if total == target:
                # If the current combination sums up to the target, add it to the result
                res.append(cur.copy())
                return
            if i >= len(candidates) or total > target:
                # If we've exceeded the array bounds or the sum is greater than the target, return
                return

            cur.append(candidates[i])  # Add the current candidate to the combination
            dfs(i, cur, total + candidates[i])  # Recursively explore with the current candidate
            cur.pop()  # Backtrack by removing the last candidate
            dfs(i + 1, cur, total)  # Recursively explore without the current candidate

        dfs(0, [], 0)  # Start the DFS from the beginning of the candidates list
        return res  # Return the list of valid combinations
```

# JavaScript
```
/**
 * Time O(N * ((Target/MIN) + 1)) | Space O(N * (Target/Min))
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
 var combinationSum = function (candidates, target, index = 0, combination = [], combinations = []) {
    const isBaseCase = target < 0;
    if (isBaseCase) return combinations;

    const isTarget = target === 0;
    if (isTarget) return combinations.push(combination.slice());

    for (let i = index; i < candidates.length; i++) {
        backTrack(candidates, target, i, combination, combinations);
    }

    return combinations;
}

const backTrack = (candidates, target, i, combination, combinations) => {
    combination.push(candidates[i]);
        combinationSum(candidates, (target - candidates[i]), i, combination, combinations);
    combination.pop();
}
```
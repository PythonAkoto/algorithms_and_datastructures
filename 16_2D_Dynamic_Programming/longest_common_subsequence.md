# 1143. Longest Common Subsequence
## Company: Google

Given two strings `text1` and `text2`, *return the length of their longest* ***common subsequence***. If there is no **common subsequence**, return 0.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

- For example, `"ace"` is a subsequence of `"abcde"`.
A **common subsequence** of two strings is a subsequence that is common to both strings.

 

Example 1:

Input: `text1 = "abcde", text2 = "ace"` 
Output: `3`  
Explanation: The longest common subsequence is `"ace"` and its length is `3`.

Example 2:

Input: `text1 = "abc", text2 = "abc"`
Output: `3`
Explanation: The longest common subsequence is `"abc"` and its length is `3`.

Example 3:

Input: `text1 = "abc", text2 = "def"`
Output: `0`
Explanation: There is no such common subsequence, so the result is `0`.

# Python
```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        # Initialize a 2D array to store the lengths of common subsequences
        dp = [[0 for j in range(len(text2) + 1)] for i in range(len(text1) + 1)]

        # Iterate through the strings in reverse order to build the DP table
        for i in range(len(text1) - 1, -1, -1):
            for j in range(len(text2) - 1, -1, -1):
                # Check if the current characters match
                if text1[i] == text2[j]:
                    # If they match, add 1 to the length of the common subsequence
                    dp[i][j] = 1 + dp[i + 1][j + 1]
                else:
                    # If they don't match, take the maximum length from the adjacent cells
                    dp[i][j] = max(dp[i][j + 1], dp[i + 1][j])

        # The result is the length of the common subsequence starting from the beginning of both strings
        return dp[0][0]
```

# JavaScript
```
// Function to find the length of the longest common subsequence using memoization
var longestCommonSubsequence = (text1, text2, p1 = 0, p2 = 0, memo = initMemo(text1, text2)) => {
    // Check if either of the strings has been fully traversed
    const isBaseCase = ((p1 === text1.length) || (p2 === text2.length));
    if (isBaseCase) return 0;

    // Check if the current subproblem has been seen before
    const hasSeen = (memo[p1][p2] !== null);
    if (hasSeen) return memo[p1][p2];

    // If not seen before, recursively explore the subproblem
    return dfs(text1, text2, p1, p2, memo); /* Time O((N * M) * M)) | Space O((N * M) + HEIGHT) */
}

// Function to initialize the memoization table
var initMemo = (text1, text2) => new Array((text1.length + 1)).fill() /* Time O(N) | Space O(N) */
    .map(() => new Array((text2.length + 1)).fill(null)); /* Time O(M) | Space O(M) */

// Recursive function to explore the subproblems and update the memoization table
var dfs = (text1, text2, p1, p2, memo) => {
    // Recursively explore the subproblem by moving to the next character in text1
    const left = longestCommonSubsequence(text1, text2, (p1 + 1), p2, memo); /* Time O(N * M) | Space O(HEIGHT) */

    // Check if the current character in text1 matches with any character in the remaining portion of text2
    const index = text2.indexOf(text1[p1], p2); /* Time O(M) */
    const isPrefix = (index !== -1);

    // If there is a match, recursively explore the subproblem by moving to the next characters in both texts
    const right = isPrefix
        ? (longestCommonSubsequence(text1, text2, (p1 + 1), (index + 1), memo) + 1) /* Time O(N * M) | Space O(HEIGHT) */
        : 0;

    // Update the memoization table with the maximum of the two cases
    memo[p1][p2] = Math.max(left, right); /* | Space O(N * M) */
    return memo[p1][p2];
}
```
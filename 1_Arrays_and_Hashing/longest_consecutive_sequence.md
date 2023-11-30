# 128. Longest Consecutive Sequence
## Company: Google

Given an unsorted array of integers `nums`, return *the length of the longest consecutive elements sequence*.

You must write an algorithm that runs in `O(n)` time.

Example 1:

Input: `nums = [100,4,200,1,3,2]`
Output: `4`
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:

Input: `nums = [0,3,7,2,5,8,4,6,0,1]`
Output: `9`

# Python
```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        # Create a set to efficiently check existence of numbers
        numSet = set(nums)
        longest = 0

        # Iterate through each number in the set
        for n in numSet:
            # Check if it's the start of a sequence
            if (n - 1) not in numSet:
                length = 1
                # Check consecutive numbers in the sequence
                while (n + length) in numSet:
                    length += 1
                # Update the longest consecutive sequence length
                longest = max(length, longest)

        # Return the length of the longest consecutive sequence
        return longest
```

# JavaScript
```
var longestConsecutive = (nums, maxScore = 0) => {
    // Create a set to efficiently check existence of numbers
    const numSet = new Set(nums); /* Time O(N) | Space O(N) */

    // Iterate through each unique number in the set
    for (const num of [...numSet]) { /* Time O(N) */
        const prevNum = num - 1;

        // Skip if the current number is not the start of a sequence
        if (numSet.has(prevNum)) continue; /* Time O(N) */

        // Initialize variables for the current number and the current score
        let [currNum, score] = [num, 1];

        // Helper function to check if there is a streak of consecutive numbers
        const isStreak = () => numSet.has(currNum + 1);

        // Iterate through the consecutive streak and update the score
        while (isStreak()) { /* Time O(N) */
            currNum++;
            score++;
        }

        // Update the maximum score if the current streak is longer
        maxScore = Math.max(maxScore, score);
    }

    // Return the maximum consecutive sequence length
    return maxScore;
}
```
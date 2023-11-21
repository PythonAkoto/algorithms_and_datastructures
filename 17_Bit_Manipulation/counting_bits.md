# 338. Counting Bits
## Compnay: Amazon

*Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` (`0 <= i <= n`), `ans[i]` is the **number of `1`'s** in the binary representation of `i`.*

 

Example 1:

Input: `n = 2`
Output: `[0,1,1]`
Explanation:
```
0 --> 0
1 --> 1
2 --> 10
```

Example 2:

Input: `n = 5`
Output: `[0,1,1,2,1,2]`
Explanation:
```
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```

# Python
```
class Solution:
    def countBits(self, n):
        # Initialize an array to store the count of set bits for each number from 0 to n
        dp = [0] * (n + 1)
        
        # Initialize an offset to keep track of the power of 2
        offset = 1

        # Iterate through each number from 1 to n
        for i in range(1, n + 1):
            # Check if the current number is the next power of 2
            if offset * 2 == i:
                offset = i
            
            # Count the set bits for the current number using the offset
            dp[i] = 1 + dp[i - offset]

        # Return the array containing the count of set bits for each number from 0 to n
        return dp
```

# JavaScript
```
// Function to count the number of set bits for numbers from 0 to n
var countBits = function (n, dp = [ 0 ]) {
    // Iterate through each number from 1 to n
    for (let i = 1; i < (n + 1); i++) {
        // Calculate the middle index and the least significant bit of the current number
        const [ mid, bit ] = [ (i >> 1), (i & 1) ];

        // Calculate the count of set bits for the current number using the middle index and bit
        const bits = (dp[mid] + bit);

        // Push the count of set bits for the current number to the dp array
        dp.push(bits);
    }

    // Return the array containing the count of set bits for each number from 0 to n
    return dp;
};
```
# 70. Climbing Stairs
### Company: Amazon

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

 

Example 1:

Input: `n = 2`
Output: `2`
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

Example 2:

Input: `n = 3`
Output: `3`
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

# Python
```
class Solution:
    def climbStairs(self, n: int) -> int:
        # If there are 1, 2, or 3 steps, there is a direct mapping between the number of steps and ways to climb them.
        if n <= 3:
            return n
        # Initialize two variables to keep track of the number of ways to climb n-1 and n-2 steps.
        n1, n2 = 2, 3

        # Iterate from 4 to n to calculate the number of ways to climb n steps using the Fibonacci sequence.
        for i in range(4, n + 1):
            # Calculate the number of ways to climb the current step by adding the ways to climb n-1 and n-2 steps.
            temp = n1 + n2
            # Update n1 and n2 to prepare for the next iteration.
            n1 = n2
            n2 = temp
        # Return the number of ways to climb n steps.
        return n2
```

# JavaScript
```
var climbStairs = (n) => {
    const isBaseCase = (n === 1);
    if (isBaseCase) return 1;

    let [ next, nextNext ] = [ 1, 2 ];

    for (let index = 3; (index <= n); index++) {/* Time O(N) */
        const temp = (next + nextNext);
        
        next = nextNext;
        nextNext = temp;
    }

    return nextNext;
};
```
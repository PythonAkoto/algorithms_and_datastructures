# 22. Generate Parentheses
## Company: Amazon

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

Example 1:

Input: `n = 3`
Output: `["((()))","(()())","(())()","()(())","()()()"]`

Example 2:

Input: `n = 1`
Output: `["()"]`

# Python 
```
from typing import List

class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        # Initialize an empty stack to keep track of the current combination
        stack = []

        # Initialize an empty list to store the valid combinations
        res = []

        # Recursive function to generate valid combinations
        def backtrack(openN, closedN):
            # If the number of open and closed parentheses is equal to n, add the current combination to the result
            if openN == closedN == n:
                res.append("".join(stack))
                return

            # If the number of open parentheses is less than n, add an open parenthesis and recurse
            if openN < n:
                stack.append("(")
                backtrack(openN + 1, closedN)
                stack.pop()

            # If the number of closed parentheses is less than the number of open parentheses, add a closed parenthesis and recurse
            if closedN < openN:
                stack.append(")")
                backtrack(openN, closedN + 1)
                stack.pop()

        # Start the recursive function with initial counts of open and closed parentheses set to 0
        backtrack(0, 0)

        # Return the list of valid combinations
        return res
```

# JavaScript
```
// Function to generate all valid combinations of parentheses for a given value of n
var generateParenthesis = (n, combos = []) => {
    // Check if the base case is reached (no remaining parentheses to add)
    const isBaseCase = (n === 0);

    // If it is the base case, add an empty string to the combinations and return
    if (isBaseCase) {
        combos.push('');
        return combos;
    }

    // Iterate through possible values of c, where c represents the number of parentheses on the left
    for (let c = 0; c < n; c++) {
        // Recursively generate combinations for the left and right parts
        for (const left of generateParenthesis(c)) {
            for (const right of generateParenthesis((n - 1) - c)) {
                // Combine the left and right parts and add to the combinations
                combos.push(`(${left})${right}`);
            }
        }
    }

    // Return the list of valid combinations
    return combos;
};
```
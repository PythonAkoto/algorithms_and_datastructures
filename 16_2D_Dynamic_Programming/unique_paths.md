# 62. Unique Paths
## Company: Google

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return the *number of possible unique paths that the robot can take to reach the bottom-right corner*.

The test cases are generated so that the answer will be less than or equal to `2 * 109`.

Example 1:

Input: `m = 3, n = 7`
Output: `28`

Example 2:

Input: `m = 3, n = 2`
Output: `3`

Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down

# Python
```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # Initialize a row with all elements set to 1
        row = [1] * n

        # Iterate through each row (except the first one)
        for i in range(m - 1):
            # Create a new row with all elements set to 1
            newRow = [1] * n
            
            # Iterate through each column in reverse order
            for j in range(n - 2, -1, -1):
                # Update the current cell with the sum of the cell to its right
                # and the cell directly below it from the previous row
                newRow[j] = newRow[j + 1] + row[j]
            
            # Update the current row to be the newly calculated row
            row = newRow
        
        # The final result is the top-left element of the last row
        return row[0]

# Time complexity: O(n * m)
# Space complexity: O(n)
```

# JavaScript
```
// Function to calculate the number of unique paths in a grid
var uniquePaths = (row, col) => {
    // Initialize an array to store the number of unique paths for each column
    const tabu = initTabu(col); /* Time O(COLS) | Space O(COLS) */

    // Perform a search to fill in the tabulation array
    search(row, col, tabu); /* Time O(ROWS * COLS) | Space O(COLS) */

    // Return the result, which is the number of unique paths for the last column
    return tabu[(col - 1)];
};

// Function to initialize the tabulation array with all elements set to 1
var initTabu = (col) => new Array(col).fill(1); /* Time O(COLS) | Space O(COLS) */

// Function to perform a dynamic programming search to fill in the tabulation array
var search = (row, col, tabu) => {
    // Iterate through each row starting from the second row
    for (let _row = 1; (_row < row); _row++) { /* Time O(ROWS) */
        // Iterate through each column starting from the second column
        for (let _col = 1; (_col < col); _col++) { /* Time O(COLS) */
            // Update the current cell with the sum of the cell to its left
            // and the cell directly above it from the previous row
            const prev = tabu[(_col - 1)];
            tabu[_col] += prev; /* Space O(COLS) */
        }
    }
}

// Time and space complexities are also provided for each function
```
# 73. Set Matrix Zeros
## Company: Meta

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

Example 1:


Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
Example 2:


Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]

# Python
```
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        # Get the number of rows and columns in the matrix
        ROWS, COLS = len(matrix), len(matrix[0])
        
        # Variable to track if the first row needs to be zeroed
        rowZero = False

        # Determine which rows/columns need to be zeroed
        for r in range(ROWS):
            for c in range(COLS):
                if matrix[r][c] == 0:
                    # If a zero is found, mark the corresponding cell in the first row and column
                    matrix[0][c] = 0
                    if r > 0:
                        matrix[r][0] = 0
                    else:
                        rowZero = True

        # Update the matrix based on the marked cells in the first row and column
        for r in range(1, ROWS):
            for c in range(1, COLS):
                if matrix[0][c] == 0 or matrix[r][0] == 0:
                    matrix[r][c] = 0

        # Check and update the first column if the first cell was originally zero
        if matrix[0][0] == 0:
            for r in range(ROWS):
                matrix[r][0] = 0

        # Check and update the first row if needed
        if rowZero:
            for c in range(COLS):
                matrix[0][c] = 0
```

# JavaScript
```
// Function to set zeroes in the matrix based on specific conditions
var setZeroes = (matrix) => {
    // Check if the first column needs to be zeroed
    const _isColZero = isColZero(matrix); /* Time O(ROWS) */

    // Set the edges of the matrix to zero based on specific conditions
    setEdgesToZero(matrix); /* Time O(ROWS * COLS) */

    // Set the cells of the matrix to zero based on specific conditions
    setCellsToZero(matrix, _isColZero); /* Time O(ROWS * COLS) */
}

// Function to check if the first column contains a zero
var isColZero = (matrix) => matrix
    .some((row) => row[0] === 0); /* Time O(ROWS) */

// Function to set the edges of the matrix to zero based on specific conditions
var setEdgesToZero = (matrix) => {
    const [ rows, cols ] = [ matrix.length, matrix[0].length ];

    // Iterate through each cell in the matrix
    for (let row = 0; (row < rows); row++) { /* Time (ROWS) */
        for (let col = 1; (col < cols); col++) { /* Time (COLS) */
            const canSet = matrix[row][col] === 0;
            if (!canSet) continue;

            // Set the corresponding cells in the first row and first column to zero
            matrix[row][0] = 0;
            matrix[0][col] = 0;
        }
    }
}

// Function to set the cells of the matrix to zero based on specific conditions
var setCellsToZero = (matrix, isColZero) => {
    const [ rows, cols ] = [ matrix.length, matrix[0].length ];

    // Iterate through each cell in the matrix in reverse order
    for (let row = (rows - 1); (0 <= row); row--) { /* Time (ROWS) */
        for (let col = (cols - 1); (1 <= col); col--) { /* Time (COLS) */
            // Check if the current cell needs to be set to zero
            if (!isZero(matrix, row, col)) continue;

            // Set the current cell to zero
            matrix[row][col] = 0;
        }

        // If the first column needs to be zeroed, set the corresponding cell to zero
        if (isColZero) matrix[row][0] = 0;
    }
}

// Function to check if a cell should be set to zero based on conditions
var isZero = (matrix, row, col) => {
    const [ rowLeftEdge, colTopEdge ] = [ matrix[row][0], matrix[0][col] ];

    // Check if the cell should be set to zero based on the edges of the matrix
    return ((rowLeftEdge === 0) || (colTopEdge === 0));
}
```
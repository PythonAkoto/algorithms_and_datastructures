# 36. Valid Sudoku
## Company: Amazon

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules:**

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

Note:
- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.
 

Example 1:
```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

Example 2:
```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
```
Explanation: Same as Example 1, except with the `5` in the top left corner being modified to `8`. Since there are two 8's in the top left 3x3 sub-box, it is invalid.

# Python
```
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        # Initialize dictionaries to keep track of numbers in each row, column, and square
        cols = collections.defaultdict(set)
        rows = collections.defaultdict(set)
        squares = collections.defaultdict(set)  # key = (r // 3, c // 3)

        # Iterate through each cell in the Sudoku board
        for r in range(9):
            for c in range(9):
                # Skip empty cells
                if board[r][c] == ".":
                    continue

                # Check if the current number is already present in the same row, column, or square
                if (
                    board[r][c] in rows[r]
                    or board[r][c] in cols[c]
                    or board[r][c] in squares[(r // 3, c // 3)]
                ):
                    return False

                # Add the current number to the sets for the corresponding row, column, and square
                cols[c].add(board[r][c])
                rows[r].add(board[r][c])
                squares[(r // 3, c // 3)].add(board[r][c])

        # If no conflicts were found, the Sudoku board is valid
        return True
```

# JavaScript
```
// Function to check the validity of a Sudoku board
var isValidSudoku = (board) => {
    const [boards, cells] = [3, 9];
    const [boxes, rows, cols] = getBoards(boards, cells); /* Time O(ROWS * COLS) | Space O(CELLS) */

    return searchGrid(board, boxes, rows, cols); /* Time O(ROWS * COLS) | Space O(CELLS) */
}

// Helper function to initialize arrays for tracking numbers in each box, row, and column
var getBoards = (boards, cells) => new Array(boards).fill()
    .map(() => new Array(cells).fill(0));

// Helper function to search through the Sudoku grid and check for valid numbers
var searchGrid = (board, boxes, rows, cols) => {
    const [_rows, _cols] = [9, 9];

    for (let row = 0; row < _rows; row++) { /* Time O(ROWS)*/
        for (let col = 0; col < _cols; col++) { /* Time O(COLS)*/
            const char = board[row][col];
            const position = 1 << (char - 1);
            const index = (Math.floor(row / 3) * 3) + Math.floor(col / 3);

            const isEmpty = char === '.';
            if (isEmpty) continue;

            const hasMoved = (boxes[index] & position) || (cols[col] & position) || (rows[row] & position);
            if (hasMoved) return false;

            // Mark the position of the current number in the corresponding box, row, and column
            rows[row] |= position; /* Space O(CELLS)*/
            cols[col] |= position; /* Space O(CELLS)*/
            boxes[index] |= position; /* Space O(CELLS)*/
        }
    }

    // If the loop completes without finding conflicts, the Sudoku board is valid
    return true;
}
```
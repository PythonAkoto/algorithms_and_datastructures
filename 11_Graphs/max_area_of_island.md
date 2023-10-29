# 695. Max Area of Island
### Company: Meta

You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected **4-directionally** (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The **area** of an island is the number of cells with a value 1 in the island.

Return the *maximum* **area** *of an island in `grid`*. If there is no island, return `0`.
 

Example 1:

Input: `grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]`
Output: `6`
Explanation: The answer is not 11, because the island must be connected 4-directionally.

Example 2:

Input: `grid = [[0,0,0,0,0,0,0,0]]`
Output: `0`

# Python 
```
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]) -> int:
        # Get the number of rows and columns in the grid.
        ROWS, COLS = len(grid), len(grid[0])
        
        # Create a set to keep track of visited cells to avoid duplicate calculations.
        visit = set()

        # Depth-first search function to calculate the area of an island starting from a cell.
        def dfs(r, c):
            # Base cases for returning 0:
            # 1. If the cell is out of bounds (row or column is less than 0 or greater/equal to ROWS or COLS).
            # 2. If the cell contains water (grid[r][c] == 0).
            # 3. If the cell has already been visited.
            if (
                r < 0
                or r == ROWS
                or c < 0
                or c == COLS
                or grid[r][c] == 0
                or (r, c) in visit
            ):
                return 0

            # Mark the current cell as visited.
            visit.add((r, c))

            # Recursively explore neighboring cells in all four directions, counting 1 for the current cell.
            return 1 + dfs(r + 1, c) + dfs(r - 1, c) + dfs(r, c + 1) + dfs(r, c - 1)

        # Initialize the maximum area to 0.
        area = 0

        # Iterate through all cells in the grid.
        for r in range(ROWS):
            for c in range(COLS):
                # For each land cell, calculate the area of the island starting from that cell,
                # and update the maximum area if needed.
                area = max(area, dfs(r, c))

        # Return the maximum area of an island found in the grid.
        return area
```

# JavaScript
```
var maxAreaOfIsland = function(grid, maxArea = 0) {
    const [ rows, cols ] = [ grid.length, grid[0].length ];
    const seen = new Array(rows).fill().map(() => new Array(cols));

    for (let row = 0; row < rows; row++) {/* Time O(ROWS) */
        for (let col = 0; col < cols; col++) {/* Time O(COLS) */
            const area = getArea(grid, row, rows, col, cols, seen);/* Space O(ROWS * COLS) */

            maxArea = Math.max(maxArea, area);
        }
    }

    return maxArea;
};

var getArea = (grid, row, rows, col, cols, seen) => {
    const isBaseCase = grid[row][col] === 0;
    if (isBaseCase) return 0;

    if (seen[row][col]) return 0;
    seen[row][col] = true;                                          /* Space O(ROWS * COLS) */

    return dfs(grid, row, rows, col, cols, seen) + 1;               /* Space O(ROWS * COLS) */
}

const dfs = (grid, row, rows, col, cols, seen, area = 0) => {
    for (const [ _row, _col ] of getNeighbors(row, rows, col, cols)) {
        area += getArea(grid, _row, rows, _col, cols, seen);
    }

    return area
} 

var getNeighbors = (row, rows, col, cols) => [[ 0, 1 ], [ 0, -1 ], [ 1, 0 ], [ -1, 0 ]]
    .map(([ _row, _col]) => [ (row + _row), (col + _col) ])
    .filter(([ _row, _col ]) => (0 <= _row) && (_row < rows) && (0 <= _col) && (_col < cols))
```
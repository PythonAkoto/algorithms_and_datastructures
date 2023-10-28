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
```
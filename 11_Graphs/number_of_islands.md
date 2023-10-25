# Number of Islands
### Company: Google

Given an `m x n` 2D binary grid grid which represents a map of `'1'`s (land) and `'0'`s (water), *return the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

Example 2:
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

# Python
```
from collections import deque

class SolutionBFS:
    def numIslands(self, grid: List[List[str]) -> int:
        if not grid:
            return 0

        rows, cols = len(grid), len(grid[0])
        visited = set()  # To keep track of visited cells
        islands = 0

        def bfs(r, c):
            q = deque()
            visited.add((r, c))
            q.append((r, c))

            while q:
                row, col = q.popleft()
                directions = [[1, 0], [-1, 0], [0, 1], [0, -1]]

                # Explore neighboring cells
                for dr, dc in directions:
                    r, c = row + dr, col + dc
                    if (
                        r in range(rows)
                        and c in range(cols)
                        and grid[r][c] == '1'
                        and (r, c) not in visited
                    ):
                        q.append((r, c))
                        visited.add((r, c))

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == "1" and (r, c) not in visited:
                    bfs(r, c)
                    islands += 1

        return islands
```

# JavaScript
```
var numIslands = function(grid, connectedComponents = 0) {
    const [ rows, cols ] = [ grid.length, grid[0].length ]

    for (let row = 0; row < rows; row++) {/* Time O(ROWS) */
        for (let col = 0; col < cols; col++) {/* Time O(COLS) */
            const isIsland = grid[row][col] === '1'
            if (isIsland) connectedComponents++

            dfs(grid, row, rows, col, cols);    /* Space O(ROWS * COLS) */
        }
    }

    return connectedComponents
};

const dfs = (grid, row, rows, col, cols) => {
    const isBaseCase = grid[row][col] === '0';
    if (isBaseCase) return;

    grid[row][col] = '0';

    for (const [ _row, _col ] of getNeighbors(row, rows, col, cols)) {
        dfs(grid, _row, rows, _col, cols);      /* Space O(ROWS * COLS) */
    }
}

var getNeighbors = (row, rows, col, cols) => [ [ 0, 1 ], [ 0, -1 ], [ 1, 0 ], [ -1, 0 ] ]
    .map(([ _row, _col ]) => [ (row + _row), (col + _col) ])
    .filter(([ _row, _col ]) => (0 <= _row) && (_row < rows) && (0 <= _col) && (_col < cols))
```
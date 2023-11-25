# 48. Rotate Image
## Company: Microsoft

You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [in-place](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

 

Example 1:

Input: `matrix = [[1,2,3],[4,5,6],[7,8,9]]`
Output: `[[7,4,1],[8,5,2],[9,6,3]]`

Example 2:

Input: `matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]`
Output: `[[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]`

# Python
```
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        l, r = 0, len(matrix) - 1
        while l < r:
            for i in range(r - l):
                top, bottom = l, r

                # save the topleft
                topLeft = matrix[top][l + i]

                # move bottom left into top left
                matrix[top][l + i] = matrix[bottom - i][l]

                # move bottom right into bottom left
                matrix[bottom - i][l] = matrix[bottom][r - i]

                # move top right into bottom right
                matrix[bottom][r - i] = matrix[top + i][r]

                # move top left into top right
                matrix[top + i][r] = topLeft
            r -= 1
            l += 1
```

# JavaScript
```
var rotate = (matrix) => {
    reverse(matrix);  /* Time O(ROWS) */
    transpose(matrix);/* Time O(ROWS * COLS) */
};

var reverse = (matrix) => matrix.reverse();

var transpose = (matrix) => {
    const rows = matrix.length;

    for (let row = 0; (row < rows); row++) {/* Time O(ROWS) */
        for (let col = 0; (col < row); col++) {/* Time O(COLS) */
            swap(matrix, row, col);
        }
    }
}

var swap = (matrix, row, col) => [matrix[row][col], matrix[col][row]] = [matrix[col][row], matrix[row][col]];
```
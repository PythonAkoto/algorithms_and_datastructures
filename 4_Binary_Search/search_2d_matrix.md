# 74. Search a 2D Matrix
### Company: Microsoft

You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.
- Given an integer target, return true if target is in matrix or false otherwise.

You must write a solution in `O(log(m * n))` time complexity.

Example 1:

Input: `matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3`
Output: `true`

Example 2:

Input: `matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13`
Output: `false`

# Python
```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        # get dimensions of the matrix by setting columns & rows
        ROWS, COLS = len(matrix), len(matrix[0])

        # create top & bottom pointers for rows in the matrix
        top, bot = 0, ROWS - 1
        
        # loop through the pointers to find the target row
        while top <= bot:
            # calculate middle row
            row = (top + bot) // 2

            # move top row down if target higher than last middle value
            if target > matrix[row][-1]:
                top = row + 1
            # move bottom row up if target lower than first middle value
            elif target < matrix[row][0]:
                bot = row - 1
            else:
                break

        # conduct binary search on the row

        # return false if target is not in row
        if not (top <= bot):
            return False

        # calculate the middle row for binary search
        row = (top + bot) // 2

        # create left and right pointers for the row
        l, r = 0, COLS - 1

        # repeat binary search on row
        while l <= r:
            # middle value for row
            m = (l + r) // 2

            # move left pointer if target higher than middle value
            if target > matrix[row][m]:
                l = m + 1

            # move right pointer if target lower than middle value
            elif target < matrix[row][m]:
                r = m - 1

            # return true if match found
            else:
                return True
        
        # return false if target never found
        return False
```

# JavaScript
```
var searchMatrix = function(matrix, target) {
    // get dimensions of the matrix
    const ROWS = matrix.length, COLS = matrix[0].length;
    // top & bottom pointers for matrix rows
    let topRow = 0, bottomRow = ROWS - 1;
    
    // loop pointers to find the target row
    while (topRow <= bottomRow) {
        // calculate middle row 
        const middleRow = Math.floor(topRow + bottomRow);
        
        // binary saerch on the rows to find target
        
        // update top row if target higher than last middle row value
        if (target > matrix[middleRow][-1]) {
            topRow = middleRow + 1;
        // update bottom row if target lower than first middle row value
        } else if (target < matrix[middleRow][0]) {
            bottomRow = middleRow - 1;
        } else {
           break; 
        }
    }
    // binary search on the last row
        
    // return false if target is not in any of the rows
    if (!(topRow <= bottomRow)) {
        return false;
    }
    
    // get middle row for binary search
    const currentMiddleRow = Math.floor(topRow + bottomRow);
    // create left and right pointers 
    let left = 0, right = COLS - 1;
    
    // repeat binary search on middle row
    while (left <= right) {
        let mid = Math.floor(left + right);
        if (target > matrix[currentMiddleRow][mid]) {
            left = mid + 1;
        } else if (target < matrix[currentMiddleRow][mid]) {
            right = mid - 1;
        } else {
            return true;
        }
    }
    return false;
};


const matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3;
console.log(searchMatrix(matrix, target));
```
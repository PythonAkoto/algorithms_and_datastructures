# 54. Spirax Matrix
## Company: Microsoft

Given an m x n matrix, return all elements of the matrix in spiral order.

Example 1:

Input: `matrix = [[1,2,3],[4,5,6],[7,8,9]]`
Output: `[1,2,3,6,9,8,7,4,5]`

Example 2:

Input: `matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]`
Output: `[1,2,3,4,8,12,11,10,9,5,6,7]`

# Python
```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        left, right = 0, len(matrix[0])
        top, bottom = 0, len(matrix)

        while left < right and top < bottom:
            # get every i in the top row
            for i in range(left, right):
                res.append(matrix[top][i])
            top += 1
            # get every i in the right col
            for i in range(top, bottom):
                res.append(matrix[i][right - 1])
            right -= 1
            if not (left < right and top < bottom):
                break
            # get every i in the bottom row
            for i in range(right - 1, left - 1, -1):
                res.append(matrix[bottom - 1][i])
            bottom -= 1
            # get every i in the left col
            for i in range(bottom - 1, top - 1, -1):
                res.append(matrix[i][left])
            left += 1

        return res
```


# JavaScript
```
var spiralOrder = (matrix, order = []) => {
    const [ rows, cols ] = [ matrix.length, matrix[0].length ];
    const cells = (rows * cols);
    let [ top, bot, left, right ] = [ 0, (rows - 1), 0, (cols - 1) ];

    while (order.length < cells) {/* Time O(ROWS * COLS) */
        traverse(
            matrix, top, bot, left, right, order
        );                        /* Time O(ROWS * COLS) | Ignore Auxilary Spsace O(ROWS * COLS) */

        top++; bot--;
        left++; right--;
    }
    
    return order;
}

var traverse = (matrix, top, bot, left, right, order) => {
    addTop(matrix, top, bot, left, right, order);  /* Time O(COLS) | Ignore Auxilary Spsace O(ROWS * COLS) */
    addRight(matrix, top, bot, left, right, order);/* Time O(ROWS) | Ignore Auxilary Spsace O(ROWS * COLS)*/
    addBot(matrix, top, bot, left, right, order);  /* Time O(COLS) | Ignore Auxilary Spsace O(ROWS * COLS)*/
    addLeft(matrix, top, bot, left, right, order); /* Time O(ROWS) | Ignore Auxilary Spsace O(ROWS * COLS. */
}

var addTop = (matrix, top, bot, left, right, order) => {
    for (let col = left; (col <= right); col++) {/* Time O(COLS) */
        order.push(matrix[top][col]);                /* Ignore Auxilary Spsace O(ROWS * COLS) */
    }
}

var addRight = (matrix, top, bot, left, right, order) => {
    for (let row = (top + 1); (row <= bot); row++) {/* Time O(ROWS) */
        order.push(matrix[row][right]);                 /* Ignore Auxilary Spsace O(ROWS * COLS) */
    }
}

var addBot = (matrix, top, bot, left, right, order) => {
    for (let col = (right - 1); (left <= col); col--) {/* Time O(COLS) */
        const isOutOfBounds = top === bot;
        if (isOutOfBounds) return;
        
        order.push(matrix[bot][col]);                      /* Ignore Auxilary Spsace O(ROWS * COLS) */
    }
}

var addLeft = (matrix, top, bot, left, right, order) => {
    for (let row = bot - 1; row >= top + 1; row--) {/* Time O(ROWS) */
        const isOutOfBounds = left === right;
        if (isOutOfBounds) return;

        order.push(matrix[row][left]);                  /* Ignore Auxilary Spsace O(ROWS * COLS) */
    }
}
```
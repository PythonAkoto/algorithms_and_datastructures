# 84. Largest Rectangle in Histogram
## Company: Google

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return *the area of the largest rectangle in the histogram*.

Example 1:

Input: `heights = [2,1,5,6,2,3]`
Output: `10`
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.

Example 2:

Input: `heights = [2,4]`
Output: `4`

# Python 
```
from typing import List

class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        # Initialize the variable to store the maximum area
        maxArea = 0

        # Initialize a stack to keep track of indices and heights
        stack = []  # Stack elements: (index, height)

        # Iterate through each bar in the histogram
        for i, h in enumerate(heights):
            start = i
            # While the stack is not empty and the current height is less than the height at the top of the stack
            while stack and stack[-1][1] > h:
                index, height = stack.pop()
                # Calculate the area of the rectangle formed by the popped bar
                maxArea = max(maxArea, height * (i - index))
                start = index
            # Push the current index and height onto the stack
            stack.append((start, h))

        # Process the remaining bars in the stack
        for i, h in stack:
            # Calculate the area of the rectangle formed by the remaining bars
            maxArea = max(maxArea, h * (len(heights) - i))

        # Return the maximum area
        return maxArea
```

# JavaScript
```
// Function to find the largest rectangle area in a histogram using divide-and-conquer
var largestRectangleArea = function(heights, left = 0, right = (heights.length - 1)) {
    // Check if the current range is a base case (empty or single element)
    const isBaseCase = right < left;
    if (isBaseCase) return 0;

    // Call the divide-and-conquer helper function
    return divideAndConquer(heights, left, right);
}

// Helper function for divide-and-conquer approach
const divideAndConquer = (heights, left, right, min = left) => {
    // Iterate through the current range to find the index of the minimum height
    for (let i = left; i <= right; i++) {
        // Check if the current height is less than the height at the current minimum index
        const isMinGreater = heights[i] < heights[min];
        if (!isMinGreater) continue;

        // Update the index of the minimum height
        min = i;
    }

    // Calculate the width of the current range
    const window = (right - left) + 1;

    // Calculate the area of the rectangle formed by the minimum height in the current range
    const area = heights[min] * window;

    // Recursively calculate the area for the left and right subranges
    const leftArea = largestRectangleArea(heights, (min + 1), right);
    const rightArea = largestRectangleArea(heights, left, (min - 1));

    // Return the maximum of the area in the current range and the areas from the left and right subranges
    return Math.max(area, leftArea, rightArea);
}
```
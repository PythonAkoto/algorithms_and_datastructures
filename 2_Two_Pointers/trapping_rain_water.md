# 42. Trapping Rain Water
## Company: Google

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

 

Example 1:


Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
Example 2:

Input: height = [4,2,0,3,2,5]
Output: 9

# Python
```
from typing import List

class Solution:
    def trap(self, height: List[int]) -> int:
        # Check if the input list is empty
        if not height:
            return 0

        # Initialize left and right pointers at the beginning and end of the list
        l, r = 0, len(height) - 1

        # Initialize variables to keep track of the maximum height on the left and right
        leftMax, rightMax = height[l], height[r]

        # Initialize a variable to store the total trapped water
        res = 0

        # Continue the loop until the left and right pointers meet
        while l < r:
            # If the height at the left pointer is smaller, move the left pointer to the right
            if leftMax < rightMax:
                l += 1
                # Update the leftMax if the current height is greater
                leftMax = max(leftMax, height[l])
                # Add the trapped water between leftMax and the current height to the result
                res += leftMax - height[l]
            else:
                # If the height at the right pointer is smaller, move the right pointer to the left
                r -= 1
                # Update the rightMax if the current height is greater
                rightMax = max(rightMax, height[r])
                # Add the trapped water between rightMax and the current height to the result
                res += rightMax - height[r]

        # Return the total trapped water
        return res
```

# JavaScript
```
// Function to calculate the trapped water given an array of heights
var trap = function (height) {
    // Initialize left and right pointers at the beginning and end of the array
    let [left, right] = [0, height.length - 1];

    // Initialize variables to keep track of the maximum heights on the left and right, and the total trapped water
    let [maxLeft, maxRight, area] = [0, 0, 0];

    // Continue the loop until the left and right pointers meet
    while (left < right) {
        // Get the heights at the left and right pointers
        const [leftHeight, rightHeight] = getHeights(height, left, right);

        // Get the trapped water in the left and right windows
        const [leftWindow, rightWindow] = getWindows(
            height,
            left,
            maxLeft,
            right,
            maxRight
        );

        // Check if the height on the right is greater than or equal to the height on the left
        const isRightGreater = leftHeight <= rightHeight;

        // If the height on the right is greater, update maxLeft and add the trapped water in the left window
        if (isRightGreater) {
            if (hasNewMax(maxLeft, leftHeight)) maxLeft = leftHeight;
            else area += leftWindow;

            left++;
        }

        // Check if the height on the right is less than the height on the left
        const isRightLess = rightHeight < leftHeight;

        // If the height on the right is less, update maxRight and add the trapped water in the right window
        if (isRightLess) {
            if (hasNewMax(maxRight, rightHeight)) maxRight = rightHeight;
            else area += rightWindow;

            right--;
        }
    }

    // Return the total trapped water
    return area;
};

// Function to check if a new maximum height is encountered
const hasNewMax = (max, height) => max < height;

// Function to get the heights at the left and right pointers
const getHeights = (height, left, right) => [height[left], height[right]];

// Function to get the trapped water in the left and right windows
const getWindows = (height, left, maxLeft, right, maxRight) => {
    const [leftHeight, rightHeight] = getHeights(height, left, right);

    // Calculate the heights of the left and right windows
    const [leftWindow, rightWindow] = [
        maxLeft - leftHeight,
        maxRight - rightHeight,
    ];

    // Return the trapped water in the left and right windows
    return [leftWindow, rightWindow];
};
```
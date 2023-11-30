# 11. Container With Most Water
## Company: Google, Meta

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

*Return the maximum amount of water a container can store.*

**Notice** that you may not slant the container.

Example 1:

Input: `height = [1,8,6,2,5,4,8,3,7]`
Output: `49`
Explanation: The above vertical lines are represented by array `[1,8,6,2,5,4,8,3,7]`. In this case, the max area of water (blue section) the container can contain is 49.

Example 2:

Input: `height = [1,1]`
Output: `1`

# Python
```
from typing import List

class Solution:
    def maxArea(self, height: List[int]) -> int:
        # Initialize left and right pointers at the two ends of the height list.
        l, r = 0, len(height) - 1
        # Initialize the variable to store the maximum area.
        res = 0

        # Continue the loop until the left pointer is less than the right pointer.
        while l < r:
            # Calculate the current area between the two pointers and update the result.
            res = max(res, min(height[l], height[r]) * (r - l))
            
            # Move the pointers towards each other based on the height of the walls.
            if height[l] < height[r]:
                l += 1
            elif height[r] <= height[l]:
                r -= 1
            
        # Return the maximum area found.
        return res
```

# JavaScript
```
var maxArea = function (height) {
    // Initialize left, right pointers, and max area.
    let [left, right, max] = [0, height.length - 1, 0];

    // Continue the loop until the left pointer is less than the right pointer.
    while (left < right) {
        // Variables to store container height and area.
        let containerHeight, area;

        // Calculate the width of the container between left and right pointers.
        let containerWidth = right - left;

        // Determine the smaller height of the two walls.
        if (height[left] < height[right]) {
            containerHeight = height[left];
            // Move the left pointer to the right.
            left++;
        } else {
            containerHeight = height[right];
            // Move the right pointer to the left.
            right--;
        }

        // Calculate the area of the current container.
        area = containerWidth * containerHeight;

        // Update the maximum area if the current area is greater.
        if (area > max) {
            max = area;
        }
    }

    // Return the maximum area found.
    return max;
};
```
# 435. Non-overlapping Intervals
## Company: Microsoft

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, *return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.*

 

Example 1:

Input: `intervals = [[1,2],[2,3],[3,4],[1,3]]`
Output: `1`
Explanation: `[1,3]` can be removed and the rest of the intervals are non-overlapping.

Example 2:

Input: `intervals = [[1,2],[1,2],[1,2]]`
Output: `2`
Explanation: You need to remove two `[1,2]` to make the rest of the intervals non-overlapping.

Example 3:

Input: `intervals = [[1,2],[2,3]]`
Output: `0`
Explanation: You don't need to remove any of the intervals since they're already non-overlapping.

# Python
```
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        # Sort intervals based on the start time
        intervals.sort()
        
        # Initialize the result variable to count overlapping intervals
        res = 0
        
        # Initialize variable to keep track of the end time of the previous interval
        prevEnd = intervals[0][1]
        
        # Iterate through the sorted intervals starting from the second interval
        for start, end in intervals[1:]:
            # Check if the current interval does not overlap with the previous one
            if start >= prevEnd:
                # Update the end time of the previous interval to the current end time
                prevEnd = end
            else:
                # If the intervals overlap, increment the result count
                res += 1
                # Choose the interval with the minimum end time to retain
                prevEnd = min(end, prevEnd)
        
        # Return the total count of overlapping intervals
        return res
```

# JavaScript
```
// Function to erase overlapping intervals
var eraseOverlapIntervals = function (intervals) {
    // Sort intervals based on end time, and if equal, then by start time
    intervals.sort(([aStart, aEnd], [bStart, bEnd]) =>
        aEnd !== bEnd ? aEnd - bEnd : aStart - bStart
    );

    // Call the helper function to get the count of non-overlapping intervals
    return getGaps(intervals);
};

// Helper function to calculate the count of non-overlapping intervals
const getGaps = (intervals, gaps = 1) => {
    // Remove the first interval from the array and consider it as the initial non-overlapping interval
    const prev = intervals.shift();

    // Iterate through the remaining intervals
    for (const curr of intervals) {
        // Destructure start and end times for both current and previous intervals
        const [prevStart, prevEnd] = prev;
        const [currStart, currEnd] = curr;

        // Check if there is a gap between the previous interval's end and the current interval's start
        const hasGap = prevEnd <= currStart;
        
        // If there is a gap, update the end time of the previous interval to the current end time
        if (!hasGap) continue;

        prev[1] = curr[1];
        gaps++;
    }

    // Calculate the count of non-overlapping intervals
    return intervals.length + 1 - gaps;
}
```
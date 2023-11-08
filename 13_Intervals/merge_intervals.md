# Merge Intervals
## Company: Microsoft

Given an array of `intervals` where `intervals[i] = [starti, endi]``, merge all overlapping intervals, and return *an array of the non-overlapping intervals that cover all the intervals in the input.*

 

Example 1:

Input: `intervals = [[1,3],[2,6],[8,10],[15,18]]`
Output: `[[1,6],[8,10],[15,18]]`
Explanation: Since intervals `[1,3]` and `[2,6]` overlap, merge them into `[1,6]`.

Example 2:

Input: `intervals = [[1,4],[4,5]]`
Output: `[[1,5]]`

# Python
```
class Solution:
    def merge(self, intervals: List[List[int]) -> List[List[int]]:
        # Sort the intervals based on the start value
        intervals.sort(key=lambda pair: pair[0])
        
        # Initialize the output list with the first interval
        output = [intervals[0]]

        # Iterate through the sorted intervals
        for start, end in intervals:
            # Get the end value of the last interval in the output list
            lastEnd = output[-1][1]

            # Check if the current interval can be merged with the last one
            if start <= lastEnd:
                # Merge the intervals by updating the end value of the last interval
                output[-1][1] = max(lastEnd, end)
            else:
                # If the current interval cannot be merged, add it as a new interval
                output.append([start, end])
        
        # Return the merged intervals
        return output
```

# JavaScript
```
var merge = function (intervals) {
    // Sort the intervals first based on the start values and then on the end values.
    intervals.sort(([aStart, aEnd], [bStart, bEnd]) =>
        aStart !== bStart ? aStart - bStart : aEnd - bEnd
    );

    return mergeIntervals(intervals);
};

const mergeIntervals = (intervals, merged = []) => {
    // Take the first interval as the initial interval for comparison.
    let prev = intervals.shift();

    for (const curr of intervals) {
        const [prevStart, prevEnd] = prev;
        const [currStart, currEnd] = curr;

        // Check if the current interval has an overlap with the previous interval.
        const hasOverlap = currStart <= prevEnd;

        if (hasOverlap) {
            // If there is an overlap, update the end value of the previous interval
            // to include the current interval.
            prev[1] = Math.max(prev[1], curr[1]);
            continue;
        }

        // If there is no overlap, push the previous interval into the merged array
        // and update the previous interval to the current interval.
        merged.push(prev);
        prev = curr;
    }

    // Push the last remaining interval (or the only interval) into the merged array.
    return [...merged, prev];
};
```
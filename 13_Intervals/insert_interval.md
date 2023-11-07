# 57. Insert Inverval
## Company: Microsoft

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

 

Example 1:

Input: `intervals = [[1,3],[6,9]], newInterval = [2,5]`
Output: `[[1,5],[6,9]]`

Example 2:

Input: `intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]`
Output: `[[1,2],[3,10],[12,16]]`

# Python
```
class Solution:
    def insert(
        self, intervals: List[List[int]], newInterval: List[int]
    ) -> List[List[int]]:
        # Initialize an empty list to store the resulting merged intervals.
        res = []

        # Iterate through each interval in the input 'intervals' list.
        for i in range(len(intervals)):
            # If the end of the 'newInterval' is less than the start of the current interval,
            # it means 'newInterval' should be inserted before the current interval.
            if newInterval[1] < intervals[i][0]:
                res.append(newInterval)  # Add 'newInterval' to the result.
                return res + intervals[i:]  # Return the result plus the remaining intervals.

            # If the start of 'newInterval' is greater than the end of the current interval,
            # it means the current interval should be added to the result as it is.
            elif newInterval[0] > intervals[i][1]:
                res.append(intervals[i])  # Add the current interval to the result.

            # If there is an overlap between 'newInterval' and the current interval,
            # merge the two intervals by updating the 'newInterval'.
            else:
                newInterval = [
                    min(newInterval[0], intervals[i][0]),  # Update the start of 'newInterval'.
                    max(newInterval[1], intervals[i][1]),  # Update the end of 'newInterval'.
                ]

        # After looping through all intervals, add the final 'newInterval' to the result.
        res.append(newInterval)

        # Return the list of merged intervals.
        return res
```

# JavaScript 
```
function insert(intervals, newInterval) {
    // Initialize an empty array to store the resulting merged intervals.
    const res = [];

    // Iterate through each interval in the input 'intervals' array.
    for (let i = 0; i < intervals.length; i++) {
        // If the end of 'newInterval' is less than the start of the current interval,
        // it means 'newInterval' should be inserted before the current interval.
        if (newInterval[1] < intervals[i][0]) {
            res.push(newInterval);  // Add 'newInterval' to the result.
            return res.concat(intervals.slice(i));  // Return the result plus the remaining intervals.
        }

        // If the start of 'newInterval' is greater than the end of the current interval,
        // it means the current interval should be added to the result as it is.
        else if (newInterval[0] > intervals[i][1]) {
            res.push(intervals[i]);  // Add the current interval to the result.
        }

        // If there is an overlap between 'newInterval' and the current interval,
        // merge the two intervals by updating the 'newInterval'.
        else {
            newInterval = [
                Math.min(newInterval[0], intervals[i][0]),  // Update the start of 'newInterval'.
                Math.max(newInterval[1], intervals[i][1])   // Update the end of 'newInterval'.
            ];
        }
    }

    // After looping through all intervals, add the final 'newInterval' to the result.
    res.push(newInterval);

    // Return the array of merged intervals.
    return res;
}
```
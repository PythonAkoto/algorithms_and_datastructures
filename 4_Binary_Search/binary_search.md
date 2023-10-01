# 704. Binary Search
### Company: Microsoft

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If target exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with O(log n) runtime complexity.

 

Example 1:

  Input: `nums = [-1,0,3,5,9,12], target = 9`
  Output: `4`
  *Explanation: 9 exists in nums and its index is 4*

Example 2:

  Input: `nums = [-1,0,3,5,9,12], target = 2`
  Output: `-1`
  *Explanation: 2 does not exist in nums so return -1*

# Python
```
def search(self, nums: List[int], target: int) -> int:
    # create left and right pointers
    l, r = 0, len(nums) - 1

    # iterate through the pointers
    while l <= r:
        # calculate the midpoint using floor division
        m = l + ((r - l) // 2)  # (l + r) // 2 can lead to overflow

        # if num higher than midpoint change right pointer
        if nums[m] > target:
            # the right pointer now updated
            r = m - 1
        
        # if num lower than midpoint update left pointer 
        elif nums[m] < target:
            l = m + 1

        # otherwise the num is found in mid point
        else:
            return m    # return index
    
    # return -1 if all fails 
    return -1
```

# JavaScript
```
var search = function(nums, target) {
    // create left and right pointers
    let left = 0, right = nums.length - 1;
    
    // search through the array using the pointers
    while (left <= right) {
        // calculate the midpoint
        const mid = left + Math.floor((right - left) / 2);
        
        // if nums higher than the midpoint, update the right pointer
        // if nums lower than midpoint, update left pointer
        if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            return mid;
        }
    }
    return -1;
};

let nums = [-1,0,3,5,9,12], target = 9;
console.log(search(nums, target));
```
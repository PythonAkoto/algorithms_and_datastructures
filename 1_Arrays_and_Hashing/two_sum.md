# 1. Two Sum
## Solution: hashmap

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:

Input: `nums = [2,7,11,15], target = 9`
Output: `[0,1]`
Explanation: Because `nums[0] + nums[1] == 9`, we return `[0, 1]`.

Example 2:

Input: `nums = [3,2,4], target = 6`
Output: `[1,2]`

Example 3:

Input: `nums = [3,3], target = 6`
Output: `[0,1]`

# Python
```
# create hashmap to add number & index 
prevMap = {}  # val -> index

# iterate through list using enumerate -> returns index,value
for i, n in enumerate(nums):
    # calculate difference (tarsget minus index value)
    diff = target - n
    # check if difference is already in hashmap
    if diff in prevMap:
        return [prevMap[diff], i]     # return pair of indecies
    # update hashmap
    prevMap[n] = i
```

# JavaScript
```
var twoSum = function(nums, target) {
    // create empty hashmap
    const prevMap = {};

    // loop list via its length
    for (let i = 0; i < nums.length; i++) {
        const n = nums[i];          // get each number from list
        const diff = target - n;    // target minus the value in each list
        
        // check if diff is in hashmap
        if (prevMap.hasOwnProperty(diff)) {
            return [prevMap[diff], i];
        }
        
        // update hashmap -> list value: list index
        prevMap[n] = i;
    }
    return null
};


// Example usage
const nums = [2, 7, 11, 15];
const target = 9;
const result = twoSum(nums, target);
console.log(result);
```
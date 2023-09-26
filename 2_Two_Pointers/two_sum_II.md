# 167. Two Sum II - Input Array is Sorted
### Company: Amazon

Given a **1-indexed** array of integers `numbers` that is already ***sorted in non-decreasing order***, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 < numbers.length`.

Return the indices of the *two numbers*, `index1` and `index2`, ***added by one*** as an *integer array* `[index1, index2]` of length 2.

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

*Your solution must use only constant extra space.*

 

Example 1:

Input: `numbers = [2,7,11,15], target = 9`
Output: `[1,2]`
*Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].*

Example 2:

Input: `numbers = [2,3,4], target = 6`
Output: `[1,3]`
*Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].*

Example 3:

Input: `numbers = [-1,0], target = -1`
Output: `[1,2]`
*Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].*


# Python
```
# create your left & right pointers
l, r = 0, len(numbers) - 1

# loop through the pointers to add values
while l < r:
    # add the two pointers together
    curSum = numbers[l] + numbers[r]

    # move right pointer if higher than target
    if curSum > target:
        r -= 1
    # move left pointer if lower than target
    elif curSum < target:
        l += 1
    else:
        return [l + 1, r + 1]
```

# JavaScript
```
var twoSum = function(numbers, target) {
     // create left and right pointers 
    let pLeft = 0, pRight = (numbers.length) - 1;
    
    // loop through the numbers array using pointers
    while (pLeft < pRight) {
        // add pointers together
        let currentSum = numbers[pLeft] + numbers[pRight];
        
        // move right pointer if current sum higher than target
        if (currentSum > target) {
            pRight -= 1;
        } else if (currentSum < target) {
            pLeft += 1;
        } else {
            return [pLeft + 1, pRight + 1];
        }
    }
};

console.log("Yaw Akoto");

let nums = [2,7,11,15], target = 9;
console.log(twoSum(nums, target));
```
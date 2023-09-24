# 217. Contains Duplicate
## Solution: hashset or pointers
### Company: Microsoft
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

 
Example 1:

Input: `nums = [1,2,3,1]`
Output: `true`

Example 2:

Input: `nums = [1,2,3,4]`
Output: `false`

Example 3:

Input: `nums = [1,1,1,3,3,4,3,2,4,2]`
Output: `true`

# Python
```
# create a hashset
hashset = set()

# loop through list to check duplicates
for num in nums:
    # check if num already exists in hashset
    if num in hashset:
        return True
    # add num to hashset
    hashset.add(num)
return False
```

# JavaScript
```
// loop through nums list
for (let right = 0; right < nums.length; right++) {
    // loop through each right pointer
    for (let left = 0; left < right; left++) { 
        // check if both pointers are duplicate
        const isDuplicate = nums[left] === nums[right];
        // return true if match is found
        if (isDuplicate) return true;
    }
}
// return false if no match 
return false;

console.log(containsDuplicate([1,2,1,3,4]))
```
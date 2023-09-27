# 15. 3Sum
### Company: Facebook

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j, i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

 

Example 1:

Input: `nums = [-1,0,1,2,-1,-4]`
Output: `[[-1,-1,2],[-1,0,1]]`
*Explanation:* 
`nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0`*.*
`nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0`*.*
`nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0`*.*
*The distinct triplets are* `[-1,0,1] and [-1,-1,2]`*.*
*Notice that the order of the output and the order of the triplets does not matter.*

Example 2:

Input: `nums = [0,1,1]`
Output: `[]`
*Explanation: The only possible triplet does not sum up to 0.*

Example 3:

Input: `nums = [0,0,0]`
Output: `[[0,0,0]]`
*Explanation: The only possible triplet sums up to 0.*

# Python
```
res = []                                                # create empty list to store results
nums.sort()                                             # sort list to accending order

# use enumerate to get index-value from list
# i=index a=number
for i, a in enumerate(nums):
    # Skip positive integers
    if a > 0:
        break
    
    # skip number if duplicate
    if i > 0 and a == nums[i - 1]:
        continue
    
    # create left & right pointers 
    l, r = i + 1, len(nums) - 1
    while l < r:
        threeSum = a + nums[l] + nums[r]                # calculate the 3 sum
        if threeSum > 0:
            r -= 1                                      # move pointer left if lower than 0
        elif threeSum < 0:
            l += 1                                      # mover pointer right if higher than 0
        else:
            res.append([a, nums[l], nums[r]])           # add correct numbers to empty list 
            
            # move pointers after each iteration
            l += 1
            r -= 1

            # if a duplicate is found, but only want to move 1 pointer (edge case)
            while nums[l] == nums[l - 1] and l < r:
                l += 1
                
return res

```

# JavaScript
```
```
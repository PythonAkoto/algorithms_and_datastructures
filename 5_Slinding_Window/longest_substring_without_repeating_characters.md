# 3. Longest Substring Without Repeating Characters
### Company: Facebook / Meta

Given a string `s`, find the length of the **longest substring** without repeating characters.

 

Example 1:

Input: `s = "abcabcbb"`
Output: `3`
*Explanation: The answer is "abc", with the length of 3.*

Example 2:

Input: `s = "bbbbb"`
Output: `1`
*Explanation: The answer is "b", with the length of 1.*

Example 3:

Input: `s = "pwwkew"`
Output: `3`
*Explanation: The answer is "wke", with the length of 3.*
*Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.*

# Python
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        # create a set to store letters
        charSet = set()
        # set left pointer to 0 (which will be first letter)
        l = 0
        # set result to 0
        res = 0

        # loop through each letter in string using right pointer
        for r in range(len(s)):
            # if the letter is in the set..
            while s[r] in charSet:
                # remove the letter from set
                charSet.remove(s[l])
                # move left pointer to next letter
                l += 1
            # add each letter to the set using right pointer
            charSet.add(s[r])
            # find max num of letters by calculating distance between left & right pointer
            res = max(res, r - l + 1)
        
        # return the result 
        return res
```

# JavaScript
```
```
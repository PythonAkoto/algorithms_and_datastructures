# 49. Group Anagrams
## Company: Amazon

Given an array of strings `strs`, group **the anagrams** together. You can return the answer **in any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:

Input: `strs = ["eat","tea","tan","ate","nat","bat"]`
Output: `[["bat"],["nat","tan"],["ate","eat","tea"]]`

Example 2:

Input: `strs = [""]`
Output: `[[""]]`

Example 3:

Input: `strs = ["a"]`
Output: `[["a"]]`

# Python
```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        # Initialize a defaultdict to store anagrams grouped by their character counts
        ans = collections.defaultdict(list)

        # Iterate through each string in the input list
        for s in strs:
            # Initialize a list to count the occurrences of each character in the string
            count = [0] * 26

            # Count the occurrences of each character in the string
            for c in s:
                count[ord(c) - ord("a")] += 1

            # Convert the count list to a tuple to use it as a key in the defaultdict
            ans[tuple(count)].append(s)

        # Return the grouped anagrams as a list of lists
        return ans.values()
```

# JavaScript
```
```
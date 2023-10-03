# 424. Longest Repeating Character Replacement
### Company: Google

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

*Return the length of the longest substring containing the same letter you can get after performing the above operations.*

 

Example 1:

Input: `s = "ABAB", k = 2`
Output: `4`
*Explanation: Replace the two 'A's with two 'B's or vice versa.*

Example 2:

Input: `s = "AABABBA", k = 1`
Output: `4`
*Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".*
*The substring "BBBB" has the longest repeating letters, which is 4.*
*There may exists other ways to achive this answer too.*

# Python
```
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        # create hashmap to count each letter
        count = {}
        
        # initialise left pointer & resut to 0
        l = 0
        maxf = 0

        # use the right pointer to loop through the letters
        for r in range(len(s)):
            # update the hashmap for each letter found
            count[s[r]] = 1 + count.get(s[r], 0)
            # update result
            maxf = max(maxf, count[s[r]])

            # check if the number of replacements needed is greater than the allowed limit (k)
            # if so, we need to shift the left pointer and adjust the counts accordingly
            # the idea is to maintain a window with the maximum repeating character within the window
            # and replace the rest, so the window length - count of the most frequent character will give us
            # the number of replacements needed

            if (r - l + 1) - maxf > k:
                # decrement the count of the character at the left pointer
                count[s[l]] -= 1
                # move the left pointer to the right
                l += 1

        # the maximum valid window length is given by the difference between the right and left pointers
        return (r - l + 1)
```

# JavaScript
```
var characterReplacement = function(s, k) {
    // create hashmap to store letters
    let hashmap = new Map();
    // initialise pointers and result
    let left = 0, maxSubstring = 0;
    
    // create right pointer to loop through each letter
    for (let right = 0; right < s.length; right++) {
        let maxWindowLength = right - left + 1;
        
        // update existing letter in hashmap or add new value
        // we use the letter of each string as the key and the value
        // is the count of each letter
        // if the key is not in the hashmap we add 0 to 1 (1 + 0))
        hashmap.set(s[right], 1 + (hashmap.get(s[right]) || 0));
        
        // check if number of replacements needed is greater than the limit
        if ((maxWindowLength - Math.max(...hashmap.values())) > k) {
            // decrement the count of the left pointer letter in hashmap
            hashmap.set(s[left], hashmap.get(s[left]) - 1);
            // move the left pointer to next letter
            left++;
        }
        // recalculate the new max window and then the max substring 
        maxWindowLength = right - left + 1;
        maxSubstring = Math.max(maxSubstring, maxWindowLength);
    }
    // return the result
    return maxSubstring;
};

const s = "ABAB", k = 2;
console.log(characterReplacement(s, k));
console.log('\nYaw Akoto');
```
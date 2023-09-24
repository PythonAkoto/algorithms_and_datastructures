# 242. Valid Anagram
## Company: Uber
An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:

Input: `s = "anagram", t = "nagaram"`
Output: `true`

Example 2:

Input: `s = "rat", t = "car"`
Output: `false`

# Python
```
# check if length of both strings match in length
if len(s) != len(t):
    return False

# create empty hashmap 
# this will count how many times each letter has in a string
countS, countT = {}, {}

# loop through both strings, add them to hashmaps
for i in range(len(s)):
    countS[s[i]] = 1 + countS.get(s[i], 0)
    countT[t[i]] = 1 + countT.get(t[i], 0)

# check if hashmaps are equal
for c in countS:
    if countS[c] != countT.get(c, 0):
        return False

return True
```

# JavaScript
```
// first check if both strings match length
if (s.length !== t.length) {
    return false;
}

/*
Now we create the empy hashmaps, which will count
how many times each letter appears in the string.
*/
const countS = {};
const contT = {};

// loop through strings, adding them to their hashmap
for (let i = 0; i < s.length; i++) {
    // this adds current letter of string to hashmap, with number of entries 
    countS[s[i]] = 1 + (countS[s[i]] || 0);
    countT[t[i]] = 1 + (countT[t[i]] || 0);
}

// check if both hashmaps are equal
for (const char in countS) {
    // checks if pairs are NOT equal
    if (countS[char] !== countT[char]) {
        return false;
    }
}
return true;

// examples
const result1 = isAnagram("anagram", "nagaram");
console.log(result1);
```
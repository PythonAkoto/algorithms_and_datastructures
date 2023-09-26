# 125. Valid Palindrome
### Company: Spotify

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

 

Example 1:

Input: `s = "A man, a plan, a canal: Panama"`
Output: `true`
*Explanation: "amanaplanacanalpanama" is a palindrome.*

Example 2:

Input: `s = "race a car"`
Output: `false`
*Explanation: "raceacar" is not a palindrome.*

Example 3:

Input: `s = " "`
Output: `true`
*Explanation: s is an empty string "" after removing non-alphanumeric characters.*
*Since an empty string reads the same forward and backward, it is a palindrome.*

# Python Solution 1
```
# create a new empty string to add letters from given word
newStr = ""

# loop through each letter to check if alphanumeric then add to newStr object
for letter in s:
    if letter.isalnum():
        newStr += letter.lower()

# reverse the letters to see if they are the same backwards
return newStr == newStr[::-1]
```
# Python Solution 2
```
# create pointers 
l, r = 0, len(s) - 1

# create a loop by iterating the pointers 
while l < r:
    # move left pointer if no number or letter found
    while l < r and not self.alphanum(s[l]):
        l += 1
    # move right pointer if no number or letter found
    while l < r and not self.alphanum(s[r]):
        r -= 1
    
    # compare the letters in L & R pointers
    if s[l].lower() != s[r].lower():
        return False
    
    # move the pointers by 1 to compare next letters
    l += 1
    r -= 1
return True

# Could write own alpha-numeric function
def alphanum(self, c):
    return (
        ord("A") <= ord(c) <= ord("Z")
        or ord("a") <= ord(c) <= ord("z")
        or ord("0") <= ord(c) <= ord("9")
    )
```

# JavaScript Solution 1
```
// create empty string to store letters
let newStr = '';

// loop through each letter of string
for (let i = 0; i < s.length; i++) {
    const char = s[i];    // this will loop each str character
    
    // check if letter is alphanumeric using regex
    if (/[a-zA-Z0-9]/.test(char)) {
        // add letter to empty string
        newStr += char.toLowerCase();
    }
}

// reverse the letters to see if palindrome
return newStr === newStr.split('').reverse().join('');
```
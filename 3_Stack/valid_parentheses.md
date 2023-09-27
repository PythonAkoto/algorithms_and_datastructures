# 20. Valid Parentheses
### Company: Facebook

Given a string s containing just the characters `'(', ')', '{', '}', '['` and `']'`, determine if the input string is valid.

An input string is valid if:

*Open brackets must be closed by the same type of brackets.*
*Open brackets must be closed in the correct order.*
*Every close bracket has a corresponding open bracket of the same type.*
 

Example 1:

Input: `s = "()"`
Output: `true`

Example 2:

Input: `s = "()[]{}"`
Output: `true`
Example 3:

Input: `s = "(]"`
Output: `false`

# Python
```
# create hashmap to open parentheses
Map = {")": "(", "]": "[", "}": "{"}
stack = []

# check if char is in hashmap
for c in s:
    # if NOT a closing parentheses
    if c not in Map:
        stack.append(c)    # add to stack
        continue
    
    # if NOT in stack OR NOT closing parentheses 
    if not stack or stack[-1] != Map[c]:
        return False
    
    # if above conditions are not met then parentheses must match
    stack.pop()

# returns true if the stack is empty 
return not stack

```

# JavaScript
```
var isValid = function(s) {
    // create hashmap
    const hashmap = {'}':'{', ']':'[', ')':'('};
    // create stack
    let stack = [];
    
    // check if char is in hashmap
    for (let index = 0; index < s.length; index++) {
        let char = s[index];
        
        // check if NOT closing paretheses
        if (!(char in hashmap)) {
            stack.push(char);
            continue;
        }
        
        // if NOT in stack OR NOT closing parethesis
        if (stack.length === 0 || stack[stack.length- 1] !== hashmap[char]) {
            return false;
        }
        
        // if the above positions are not met then we have a match!
        stack.pop();
    }
    // returns true is the stack is empty
    return stack.length === 0;
};

let s = '()[]{}';
console.log(isValid(s))
```
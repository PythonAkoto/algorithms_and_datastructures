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
    
    # if NOT in stack AND NOT closing parentheses 
    if not stack or stack[-1] != Map[c]:
        return False
    
    # if above conditions are not met then parentheses must match
    stack.pop()

# returns true if the stack is empty 
return not stack

```

# JavaScript
```
```
# 150. Evaluate Reverse Polish Notation
### Company: Amazon

You are given an array of strings tokens that represents an arithmetic expression in a **Reverse Polish Notation**.

Evaluate the expression. Return an integer that represents the value of the expression.

*Note that:*

- The valid operators are `'+'`, `'-'`, `'*'`, and `'/'`.
- Each operand may be an integer or another expression.
- The division between two integers always **truncates toward zero**.
- There will not be any division by zero.
- The input represents a valid arithmetic expression in a reverse polish notation.
- The answer and all the intermediate calculations can be represented in a **32-bit** integer.
 

Example 1:

Input: `tokens = ["2","1","+","3","*"]`
Output: `9`
*Explanation: ((2 + 1) * 3) = 9*

Example 2:

Input: `tokens = ["4","13","5","/","+"]`
Output: `6`
*Explanation: (4 + (13 / 5)) = 6*

Example 3:

Input: `tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]`
Output: `22`
*Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5*
*= ((10 * (6 / (12 * -11))) + 17) + 5*
*= ((10 * (6 / -132)) + 17) + 5*
*= ((10 * 0) + 17) + 5*
*= (0 + 17) + 5*
*= 17 + 5*
*= 22*

# Python
```
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        # create stack
        stack = []
        for c in tokens:
            if c == "+":
                # pop twice then add sum to stack
                stack.append(stack.pop() + stack.pop())
            elif c == "-":
                # pop twice then subtract values
                a, b = stack.pop(), stack.pop()
                # force the subraction order of values
                stack.append(b - a)
            elif c == "*":
                # pop twice then multiply sum to stack
                stack.append(stack.pop() * stack.pop())
            elif c == "/":
                # pop twice then divide values
                a, b = stack.pop(), stack.pop()
                # convert whole sum to int to round down to 0
                stack.append(int(float(b) / a))
            else:
                # convert character to a number
                stack.append(int(c))
        # return result in stack
        return stack[0]
```

# JavaScript
```
```
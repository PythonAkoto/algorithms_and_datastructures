# 155. Min Stack
### Company: Amazon

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element val onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.
*You must implement a solution with O(1) time complexity for each function.*

 

Example 1:

Input
`["MinStack","push","push","push","getMin","pop","top","getMin"]`
`[[],[-2],[0],[-3],[],[],[],[]]`

Output
`[null,null,null,null,-3,null,0,-2]`

*Explanation*
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

# Python
```
class MinStack:
    def __init__(self):
        # create 2 stacks 
        self.stack = []
        self.minStack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        # check smallest value before adding to min stack 
        val = min(val, self.minStack[-1] if self.minStack else val)
        self.minStack.append(val)

    def pop(self) -> None:
        self.stack.pop()
        self.minStack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.minStack[-1]

```

# JavaScript
```
class MinStack {
    /**
     * @constructor
     */
    constructor () {
        this.stack = [];
        this.minStack = [];
    }

    /**
     * @param {number} val
     * @return {void}
     */
    push (val, { minStack } = this) {
        this.stack.push(val);             /* Space O(N) */

        const isMinEmpty = !minStack.length;
        const hasNewMin = val <= this.top(minStack);
        const canAddMin = isMinEmpty || hasNewMin;
        if (canAddMin) minStack.push(val);/* Space O(N) */
    }

    /**
     * @return {void}
     */
    pop ({ stack, minStack } = this) {
        const top = stack.pop();          /* Time O(1) */

        const canPopMin = top === this.getMin();
        if (canPopMin) minStack.pop();    /* Time O(1) */
    }

    /**
     * @param {Array}
     * @return {number}
     */
    top (stack = this.stack) {
        return stack.length
            ? stack[stack.length - 1]     /* Time O(1) */
            : null;
    }

    /**
     * @return {number}
     */
    getMin (minStack = this.minStack) {
        return this.top(minStack);       /* Time O(1) */
    }
}

```
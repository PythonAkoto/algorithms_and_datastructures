# 104. Maximum Depth of Binary Tree
### Company: Amazon

Given the `root` of a binary tree, return *its maximum depth*.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

 
Example 1:

Input: `root = [3,9,20,null,null,15,7]`
Output: `3`

Example 2:

Input: `root = [1,null,2]`
Output: `2`

# Python Solution 1 (recursive)
```
# RECURSIVE DFS
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        # return 0 if root empty
        if not root:
            return 0
        
        # pass left & right side of tree and repeat process
        # add + 1 becuase count start from 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```

# Python Solution 2 (iterative)
```
# ITERATIVE DFS
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        # initialise root with 1st node & its depth of 1
        stack = [[root, 1]]
        res = 0

        # while stack is not empty 
        while stack:
            # remove node & current depth from stack
            node, depth = stack.pop()

            # make sure the node is not empty
            if node:
                res = max(res, depth)                   # get max result 
                stack.append([node.left, depth + 1])    # add left children & update depth to stack
                stack.append([node.right, depth + 1])   # add right children & update depth to stack
        
        # return result 
        return res
```

# JavaScript
```
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
    // return 0 if root empty
    if (!root) {
        return 0;
    }

    // recursive calls
    return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
};

const root = [3,9,20,null,null,15,7];
console.log(maxDepth(root));
console.log('Yaw Akoto');
```
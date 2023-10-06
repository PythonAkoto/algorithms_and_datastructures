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
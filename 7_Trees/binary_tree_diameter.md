# 543. Diameter of Binary Tree
### Comany: Google

Given the `root` of a binary tree, return *the length of the* **diameter** *of the tree*.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The **length** of a path between two nodes is represented by the number of edges between them.

Example 1:

Input: `root = [1,2,3,4,5]`
Output: `3`
*Explanation: 3 is the length of the path* `[4,2,1,3]` *or* `[5,2,1,3]`*.*

Example 2:

Input: `root = [1,2]`
Output: `1`

# Python
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
    """
    diameter = left height + right height + 2 (plus 2 for both edges from left and right tree)
    max height = max(left, right) + 1
    """
        # create a global result variable to pass through nested func
        res = [0]

        # depth of search func
        def dfs(root):

            # if root is empty
            if not root:
                return -1
            
            # find height of left & right subtree
            left = dfs(root.left)
            right = dfs(root.right)

            # find diameter of current root
            # if the left & right height greater than result, we update the result
            res[0] = max(res[0], 2 + left + right)

            # return the height running through root node
            return 1 + max(left, right)

        # call the function passing the root
        dfs(root)

        # return result
        return res[0]
```

# JavaScript
```
```
# 226. Invert Binary Tree
### Company: Google

Given the `root` of a binary tree, invert the tree, and return its root.

Example 1:


Input: `root = [4,2,7,1,3,6,9]`
Output: `[4,7,2,9,6,3,1]`

Example 2:


Input: `root = [2,1,3]`
Output: `[2,3,1]`

Example 3:

Input: `root = []`
Output: `[]`

# Python
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None
        
        # swap the children
        root.left, root.right = root.right, root.left
        
        # make 2 recursive calls
        self.invertTree(root.left)
        self.invertTree(root.right)
        return root
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
 * @return {TreeNode}
 */
var invertTree = function(root) {
    // check if binary tree is empty
    if (!root) {
        return null;
    }

    // swap the subtrees
    let temp = root.left;           // create new var to store left val
    root.left = root.right;         // change left val to right val
    root.right = temp;              // change right val to left val

    // make recursive calls to keep swapping children
    invertTree(root.left);
    invertTree(root.right);

    return root;
};

const root = [4,2,7,1,3,6,9];
console.log(invertTree(root));
console.log('Yaw Akoto');
```
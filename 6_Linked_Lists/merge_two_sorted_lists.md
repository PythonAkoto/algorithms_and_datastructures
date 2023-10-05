# 21. Merge Two Sorted Lists
### Company: Microsoft

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

*Return the head of the merged linked list.*

 

Example 1:


Input: `list1 = [1,2,4], list2 = [1,3,4]`
Output: `[1,1,2,3,4,4]`

Example 2:

Input: `list1 = [], list2 = []`
Output: `[]`

Example 3:

Input: `list1 = [], list2 = [0]`
Output: `[0]`

# Python
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

# Iterative
class Solution:
    def mergeTwoLists(self, list1: ListNode, list2: ListNode) -> ListNode:
    # Create a dummy node to serve as the head of the merged list
    dummy = node = ListNode()

    # Iterate through both lists until at least one of them is empty
    while list1 and list2:
        # Compare the values of the current nodes from both lists
        if list1.val < list2.val:
            # Connect the smaller node to the merged list
            node.next = list1
            # Move to the next node in list1
            list1 = list1.next
        else:
            # Connect the smaller node to the merged list
            node.next = list2
            # Move to the next node in list2
            list2 = list2.next

        # Move to the next node in the merged list
        node = node.next

    # Connect the remaining nodes from the non-empty list
    node.next = list1 or list2

    # Return the merged list starting from the actual head (not the dummy node)
    return dummy.next
```

# JavaScript
```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function(list1, list2) {
    // create dummy node - this will be the head of the merged list
    let node = new ListNode();
    let dummy = node;
    
    // loop until one is empty
    while (list1 && list2) {
        // compare the val of current nodes
        if (list1.val < list2.val) {
            // add smallest node to merged list
            node.next = list1;
            // move to next node in list1
            list1 = list1.next;
        } else {
            node.next = list2;
            // move to next node in list2
            list2 = list2.next;
        }
        // move to the next node in merged list
        node = node.next;
    }
    // connect the remaining nodes from non-empty list
    node.next = list1 || list2;
    
    // return merged list, starting from actual head (not dummy node)
    return dummy.next;
};

const list1 = [1,2,4], list2 = [1,3,4];
console.log(mergeTwoLists(list1, list2));
console.log("Yaw Akoto");
```
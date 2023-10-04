# 206. Reverse Linked List
### Company: Google / Meta

Given the `head` of a singly linked list, reverse the list, and return the reversed list.

 

Example 1:

Input: `head = [1,2,3,4,5]`
Output: `[5,4,3,2,1]`

Example 2:

Input: `head = [1,2]`
Output: `[2,1]`

Example 3:

Input: `head = []`
Output: `[]`

# Python
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None


class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # create two pointers to loop through the nodes
        prev, curr = None, head

        # Traverse the list while there's a node to process (curr is not None)
        while curr:
            # Store the next node in a temporary variable (temp)
            temp = curr.next
            # Reverse the link to the previous node
            curr.next = prev
            # Move prev and curr one step forward
            prev = curr
            curr = temp

        # At the end of the loop, prev will be the new head of the reversed list
        return prev
```

# JavaScript
```
```
# 143. Reorder List
### Company: LinkedIn

You are given the head of a singly linked-list. The list can be represented as:

```
L0 → L1 → … → Ln - 1 → Ln
```

Reorder the list to be on the following form:

```
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
```
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

 

Example 1:


Input: `head = [1,2,3,4]`
Output: `[1,4,2,3]`

Example 2:


Input: `head = [1,2,3,4,5]`
Output: `[1,5,2,4,3]`

# Python
```
class Solution:
    def reorderList(self, head: ListNode) -> None:
        # find middle
        slow, fast = head, head.next
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # reverse second half
        secondHalf = slow.next
        prev = slow.next = None
        while secondHalf:
            tmp = secondHalf.next
            secondHalf.next = prev
            prev = secondHalf
            secondHalf = tmp

        # merge two halfs
        firstHalf, secondHalf = head, prev
        while secondHalf:
            tmp1, tmp2 = firstHalf.next, secondHalf.next
            firstHalf.next = secondHalf
            secondHalf.next = tmp1
            firstHalf, secondHalf = tmp1, tmp2
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
 * @param {ListNode} head
 * @return {void} Do not return anything, modify head in-place instead.
 */
var reorderList = function(head) {
    // handle cases where list has 0, 1 or 2 nodes
    if (!head || !head.next || !head.next.next) {
        return
    }
    
    // find the middle 

    // create pointers that will loop through nodes
    let slowPointer = head, fastPointer = head;
    while (fastPointer.next && fastPointer.next.next) {
        slowPointer = slowPointer.next;
        fastPointer = fastPointer.next.next;
    }
    
    // reverse 2nd half of list node
    
    let secondHalf = slowPointer.next;
    slowPointer.next = null;
    let previousNode = null;
    
    while (secondHalf) {
        let tempNode = secondHalf.next;
        secondHalf.next = previousNode;
        previousNode = secondHalf;
        secondHalf = tempNode;
    }
    
    // merge two halfs
    let firstHalf = head;
    secondHalf = previousNode;
    
    while (secondHalf) {
        let tempNode1 = firstHalf.next;
        let tempNode2 = secondHalf.next;

        firstHalf.next = secondHalf;
        secondHalf.next = tempNode1;

        firstHalf = tempNode1;
        secondHalf = tempNode2;
    }
    
};

const head = [1,2,3,4];
console.log(reorderList(head));
console.log('Yaw Akoto);
```
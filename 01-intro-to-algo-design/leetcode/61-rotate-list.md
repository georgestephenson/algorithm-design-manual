# 61. Rotate List

https://leetcode.com/problems/rotate-list

At first I solved this by storing nodes in a list

``` python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def rotateRight(self, head, k):
        """
        :type head: Optional[ListNode]
        :type k: int
        :rtype: Optional[ListNode]
        """
        if head is None:
            return None
        if head.next is None:
            return head
        nodes = []
        node = head
        while node.next is not None:
            nodes.append(node)
            node = node.next
        nodes.append(node)

        r = k % len(nodes)
        if r == 0:
            return head

        nodes[-r-1].next = None
        nodes[-1].next = nodes[0]
        return nodes[-r]
```

As usual, it's faster to do without a list and use pointers

``` python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def rotateRight(self, head, k):
        """
        :type head: Optional[ListNode]
        :type k: int
        :rtype: Optional[ListNode]
        """
        if head is None:
            return None
        if head.next is None:
            return head

        # get tail of list
        node = head
        n = 1
        while node.next is not None:
            n += 1
            node = node.next

        # get index to slice
        r = k % n

        # if we're slicing the start, no need to do anything
        if r == 0:
            return head

        # otherwise point tail at head
        node.next = head

        # traverse to slice point
        node = head
        m = n - r - 1
        while m > 0:
            node = node.next
            m -= 1
        
        # do the slice
        temp = node.next
        node.next = None
        return temp
```

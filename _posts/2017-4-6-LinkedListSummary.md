---
layout: post
title: Linked List Summary
categories:  [blog ]
tags: [Leetcode ]
comments: true
published: true


---
## Linked List Summary

Leetcode [Linked-List]( https://leetcode.com/tag/linked-list/)

1.**Delete Node in a Linked List**

- Code:

  ```python
  # Definition for singly-linked list.
  # class ListNode(object):
  #     def __init__(self, x):
  #         self.val = x
  #         self.next = None

  class Solution(object):
      def deleteNode(self, node):
          """
          :type node: ListNode
          :rtype: void Do not return anything, modify node in-place instead.
          """
          node.val = node.next.val
          node.next = node.next.next
  ```


2.**Reverse Linked List**

需要首先生成一个dummy node作为首节点。

- *dummy = ListNode*

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(0)
        while head:
            next = head.next
            head.next = dummy.next
            dummy.next = head
            head = next
        return dummy.next
```

3.**Given a singly linked list, determine if it is a palindrome.**

- 思路：
  - 找到linked list的中点。
  - 将linked list的后半部分翻转。
  - 比较前半部分与翻转后的后半部分。
- Code

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if head is None or head.next is None:
            #print head.val
            return True
        fast, slow = head, head
        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next
        fast = slow.next
        slow.next = None
        dummy = None
        while fast.next:
            next = fast.next
            fast.next = dummy
            dummy = fast
            fast = next
        fast.next = dummy
        #slow.next = dummy
        slow = head
        while fast:
            print slow.val, fast.val
            if slow.val != fast.val:
                return False
            slow, fast = slow.next, fast.next
        return True
```


​            
​        
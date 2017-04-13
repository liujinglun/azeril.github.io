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


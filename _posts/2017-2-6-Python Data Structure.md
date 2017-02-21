---
layout: post
title: Python
categories:  [blog ]
tags: [Leetcode ]
comments: true
published: true


---

# Python Data Structure

## 1.Hash Map

​	tem = dict()

Python中的Hashmap是dict。



```python
class Solution(object):
    def majorityElement(self, nums):
        tem = dict()
        if len(nums) == 1:
            return nums[0]
    		for i in nums:
        		if tem.has_key(i):
            		tem[i] += 1
            		if tem[i] > len(nums)/2:
                		return i
        else:
            tem[i] = 1
```

## 2.Hash Set

A set is an unordered collection with no duplicate elements.Basic uses include membership testing and eliminating duplicate entries.



```python
class Solution(object):
    """
    :type nums: List[int]
    :type k: int
    :rtype: bool
    """
    def containsNearbyDuplicate(self, nums, k):
    	tem = {}
    	for i, j in enumerate(nums):
        	if j in tem and abs(i-tem[j]) <= k:
            	return True
        	tem[j] = i
    	return False
```
## 3.Cache
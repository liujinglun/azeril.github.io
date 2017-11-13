---
layout: post
title: Time Complexity Summary
categories:  [blog ]
tags: [Leetcode ]
comments: true
published: true
---
## Time Complexity Summary

##### 1.Summary for Sorting Algorithm

- Insertion Sort
  - Avg: O(n^2)
  - Worst: O(n^2)
  - Best: O(n)
  - Space: O(1)
- Shell Sort
  - Avg: O(n^1.3)
  - Space: O(1)


- Bubble sort
  - Avg: O(n^2)
  - Worst: O(n^2)
  - Best: O(n)
  - Space: O(1) 
- Quicksort
  - Avg: O(n* log n)
  - Worst: O(n^2)
  - Best: O(n* log n)
  - Space: O(log n)
- Selection sort
  - Avg: O(n^2)
  - Worst: O(n^2)
  - Best: O(n^2)
  - Space: O(1)
- Heapsort
  - Avg: O(n* log n)
  - Worst: O(n* log n)
  - Best: O(n* log n)
  - Space: O(1)
- Merge sort
  - Avg: O(n* log n)
  - Worst: O(n* log n)
  - Best: O(n* log n)
  - Space: O(n)


##### 2.Stability

- Stable
  - Merge sort
  - Insertion sort
  - Bubble sort
- Unstable
  - Quicksort
  - Heapsort
  - Selection sort
  - Shell sort

##### 3.Code

- Insertion Sort


```python

```

- Merge Sort

```python
def mergesort(seq):
	if len(seq) <= 1:
		return seq
	mid = int(len(seq)/2)
	left = mergesort(seq[:mid])
	right = mergesort(seq[mid:])
	return merge(left, right)
def merge(left, right):
	result = []
	i = 0
	j = 0
	while i < len(left) and j < len(right):
		if left[i] <= right[j]:
			result.append(left[i])
			i += 1
		else:
			result.append(right[j])
			j += 1
	result += left[i:]
	result += right[j:]
	return result
a = [1, 2, 6, 5, 5, 8, 9]
print mergesort(a)
```


---
layout: post
title: Leetcode102 Python
categories: [blog]
tags:[leetcode, Binary Tree]
comments: ture
publised:true

---

## 题目要求:Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

这道题之前使用C++完成过一次，最近在学Python，所以想重新用Python再写一遍，没想到写的过程及其不顺利，费了很大劲才AC，于是记录一下。

这道题使用list的数据结构，即先将根节点放入list中，然后将根节点pop掉并且放入左右节点，然后依次进行下去。题目的难点是需要将每一层的节点作为list记录下来，而不能写到一个list中，即返回的内容是**list<list<int>>**的数据类型。为了满足以上要求，在Python代码中引入了一个名为hh的临时list用于临时存储每一层的节点信息，在每一层遍历完之后，将每一层的节点信息返回给保存节点的list,取名为node.此外，在对最终结果进行反转的时候，可以使用**result[::-1]**的方法。下面是代码信息：

```python
class Solution(object):
def levelOrder(self, root):
    """
    :type root: TreeNode
    :rtype: List[List[int]]
    """
    node = []
    result = []
    if not root:
        return []
    node.append(root)
    while node:
        tem = []
        # tem record the node in every level
        hh = []
        ## hh record the level info
        for p in node:
            tem.append(p.val)
            if p.left:
                hh.append(p.left)
            if p.right:
                hh.append(p.right)
        result.append(tem)
        node = hh[:]
    return result
```

​       PS:现在是国内的国庆期间，希望我的家人一切都好，咱们年底见。
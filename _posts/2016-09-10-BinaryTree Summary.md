---
layout: post
title: BinaryTree Summary
categories:  [blog ]
tags: [leetcode ]
comments: true
published: true
---
# 二叉树知识点总结
1.二叉搜索树：**每个节点都不比它左子树的任意元素小，而且不比它的右子树的任意元素大。**<br/>
<center>
    <p><img src="http://ww2.sinaimg.cn/large/6add1635gw1f7qi9piv80j20dw09udg4.jpg" align="center"></p>
</center>

2.二叉树节点定义：<br/>

	 struct BinaryTreeNode {
	 	int value;
	 	BinaryTreeNode* left;
	 	BinaryTreeNode* right;
	 }

3.求二叉树中节点的数量：
递归解法：<br/>
如果二叉树为空，则节点个数为0；<br/>
如果二叉树不为空，则节点个数为:**左子树节点个数+右子树节点个数+1**；

    int BinaryTree::size(Node* leaf) {
    	if (leaf == null) {
    		return 0;
    	} else {
    		return size(leaf->getleft()+leaf->getright())+1;
    	}
    }

4.求二叉树的深度：<br/>
如果二叉树为空，则深度为0；<br/>
如果二叉树不为空，则深度为**max(左子树节点个数, 右子树节点个数)+1**;

    int BinaryTree::getDepth(Node* root) {
         if (root == null) {
     	      return 0;  
     	  }
     	  int depthLeft = getDepth(root->left);
     	  int depthRight = getDepth(root->right);
     	  //return depthLeft>depthRight?(depthLeft+1):(depthRight+1);
     	  return max(depthLeft, depthRight) + 1;
     }

5.前序遍历，中序遍历，后序遍历<br/>
5.1 前序遍历  **根左右**<br/>
(1)如果二叉树为空，进行空操作.<br/>
(2)如果二叉树不为空，先访问根节点，然后访问左子树，然后右子树；<br/>

    void PreOrderTraverse(BinaryTreeNode * root) {
        if (!root)
        	return ;
        	visit(root);//visit the root node
        	PreOrderTraverse(root->left);
        	PreOrderTraverse(root->right);
    } 

 <br/>
5.2 中序遍历  **左根右**<br/>
(1)如果二叉树为空，进行空操作.<br/>
(2)如果二叉树不为空，中序遍历左子树，访问根节点，中序遍历右子树<br/>

    void PreOrderTraverse(BinaryTreeNode * root) {
    	if (!root)
    		return ;
       PreOrderTraverse(root->left);
       visit(root);//visit the root node
       PreOrderTraverse(root->right);
    }

<br/>
5.3 后序遍历  **左右根**<br/>
(1)如果二叉树为空，空操作.<br/>
(2)如果二叉树不为空，后序遍历左子树，后序遍历右子树，访问根节点.<br>

    void PreOrderTraverse(BinaryTreeNode * root) {
    		if (!root)
    			return ;
       	PreOrderTraverse(root->left);
       	PreOrderTraverse(root->right);
       	visit(root);//visit the root node
    }


<br/>
6.分层遍历二叉树<br/>
按照层次遍历二叉树，即使用上->下，左->右的顺序遍历二叉树。<br/>
相当于广度优先搜索，使用队列的数据结构。队列初始化，先把根节点放入队列中。**当队列不为空时**，进行如下操作：弹出一个节点，访问，若其左节点或者右节点不为空，则将其押入队列。<br/>
**Code**:

    void LevelTraverse(BinaryTreeNode * root) {
    	if (root == NULL) {
    		return ;
    	}
    	queue<BinaryTreeNode* > q;
    	q.push(root);
    	while (!q.empty()) {
    		BinaryTreeNode* node = q.front();
    		q.pop();
    		if (node->left != NULL) {
    			q.push(node->left);
    		}
    		if (node->right != NULL) {
    			q.push(node->right);
    		}
    		
    	}
    }

7.判断两个二叉树是否一致：

使用递归方法，先判断两个二叉树根节点是否一致，若一致，则使用左右子树分别表示根节点进行判断。

# Definition for a binary tree node.

```python
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
class Solution(object):
    def isSameTree(self, p, q):
    """
    :type p: TreeNode
    :type q: TreeNode
    :rtype: bool
    """
    if not p and not q:
    	return True
    if p and q:
    	#print 'True'
    	return (p.val == q.val) and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
    return False
if name == 'main':
    p = TreeNode(1)
    q = TreeNode(1)
    p.left = TreeNode(2)
    q.left = TreeNode(2)
    Solution().isSameTree(p, q)
```

8.**Leetcode 404. Sum of Left Leaves**

Find the sum of all left leaves in a given binary tree.

#### Analysis:

- Recursion:

  ​	判断当前节点的状态，如果**当前节点的左子树存在且当前节点左子树的左右子树均不存在**，则获取当前节点左子树的数值。之后对当前节点的左右子树分别进行同样的操作。

- Iteration

  ​	可看做binary tree的层次遍历，使用queue的数据结构，首先将root节点加入到queue中，并弹出queue的头节点(root节点信息在被记录之后弹出)。判断root的左右子树是否符合要求，如果符合要求则记录下数值，不符合要求则将root的左右子树加入到queue中，继续判断。

#### Code:

- Recursion:

  ```python
  class Solution(object):
  	def sumOfLeftLeaves(self, root):
      	"""
      	:type root: TreeNode
      	:rtype: int
      	"""
      	#recursion
      	value = 0
      	if root:
      	l, r = root.left, root.right
      	if l and l.left is None and l.right is None:
      		value += l.val
      		value += self.sumOfLeftLeaves(l) + self.sumOfLeftLeaves(r)
      	return value
  ```

- Iteration:



```python
class Solution(object):
	def sumOfLeftLeaves(self, root):
    	"""
   	 	:type root: TreeNode
   	 	:rtype: int
    	"""
    #iteration
    #hierarchical traverse of binary tree.
    	if root is None:
    		return 0
    	queue = []
    	value = 0
    	queue.append(root)
    	while queue:
        	target = queue[0]
        	queue.remove(target)
        	if target.left and target.left.left is None and target.left.right is None:
            	value += target.left.val
        	if target.left:
            	queue.append(target.left)
        	if target.right:
            	queue.append(target.right)
    	return value
```
9.Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

题目要求从右侧观察二叉树，输出看到的节点。即输出二叉树每一层中的最右侧节点。应该对二叉树进行层次遍历，并输出每一层的最后一个节点。使用queue的数据结构，并对二叉树的每一层节点个数进行计数。使用两个while循环完成。
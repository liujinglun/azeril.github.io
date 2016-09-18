---
layout: post
title: BinaryTree Summary
categories:  [blog ]
tags: [leetcode ]
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
5.1 前序遍历  ** 根左右 **<br/>
(1)如果二叉树为空，进行空操作.<br/>
(2)如果二叉树不为空，先访问根节点，然后访问左子树，然后右子树；<br/>

    void PreOrderTraverse(BinaryTreeNode * root) {
        if (!root)
        	return ;
        	visit(root);//visit the root node
        	PreOrderTraverse(root->left);
        	PreOrderTraverse(root->right);
    }
    
    
5.2 中序遍历  ** 左根右 **<br/>
(1)如果二叉树为空，进行空操作.<br/>
(2)如果二叉树不为空，中序遍历左子树，访问根节点，中序遍历右子树<br/>
 
    void PreOrderTraverse(BinaryTreeNode * root) {
    	if (!root)
    		return ;
       PreOrderTraverse(root->left);
       visit(root);//visit the root node
       PreOrderTraverse(root->right);
    }
5.3 后序遍历  ** 左右根 **<br/>
(1)如果二叉树为空，空操作.<br/>
(2)如果二叉树不为空，后序遍历左子树，后序遍历右子树，访问根节点.<br>

    void PreOrderTraverse(BinaryTreeNode * root) {
    		if (!root)
    			return ;
       	PreOrderTraverse(root->left);
       	PreOrderTraverse(root->right);
       	visit(root);//visit the root node
    }
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




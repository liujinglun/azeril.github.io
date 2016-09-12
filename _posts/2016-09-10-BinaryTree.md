---
layout: post
title: Binary Tree Summary
categories:  [blog]()
tags: [leetcode ]()
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
     	  return depthLeft>depthRight?(depthLeft+1):(depthRight+1);
	 }
	 
5.前序遍历，中序遍历，后序遍历


---
layout : post 
category : LeetCode
desc : ''
title : Invert Binary Tree
subtitle : 翻转二叉树
catalog: true
author: "Eric"
tags:
   - LeetCode
   - Java
   - Go
---


## 226.Invert Binary Tree

### 题目介绍
https://leetcode.com/problems/invert-binary-tree/description/

Given the root of a binary tree, invert the tree, and return its root.


### 例子1:
![image](/img/leetcode/invert1-tree.jpeg)
```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```

### 例子2:
![image](/img/leetcode/invert2-tree.jpeg)
```
Input: root = [2,1,3]
Output: [2,3,1]
```

## 思路
* 使用递归;
* 从根节点开始;
* 交换Left和Right两个节点的位置;

### java
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public TreeNode invertTree(TreeNode root) {
    if (root == null) {
        return null;
    }
    swap(root, root.left, root.right);
    invertTree(root.left);
    invertTree(root.right);
    return root;
}

public void swap(TreeNode root, TreeNode left, TreeNode right) {
    root.left = right;
    root.right = left;
}
```

### python
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

def invertTree(self, root: TreeNode) -> TreeNode:
    if root is None:
        return None

    root.left, root.right = root.right, root.left
    self.invertTree(root.left)
    self.invertTree(root.right)
    return root
```

### go
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func invertTree(root *TreeNode) *TreeNode {
	if root == nil {
		return nil
	}
	root.Left, root.Right = root.Right, root.Left
	invertTree(root.Left)
	invertTree(root.Right)
	return root
}
```

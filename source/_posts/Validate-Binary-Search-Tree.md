---
title: Validate Binary Search Tree
date: 2016-04-29 18:42:45
tags:
---

### Title ###
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys less than the node's key.
* The right subtree of a node contains only nodes with keys greater than the node's key.
* Both the left and right subtrees must also be binary search trees.

Tag: Tree, Deep-first Search

<br/><br/>

### Solution ###
这里有三个判断条件：

* 树中当前节点的左子树中的值小于当前节点的值
* 树中当前节点的右子树中的值大于当前节点的值
* 左右子树也满足以上两条性质

这道题有一个`误区`，我们很容易把题意理解为左孩子小于当前值并且右孩子大于当前值。<br/>

                5
              /   \
             2     6      左图满足左孩子小于当前值，并且右孩子大于当前值。但它不是二叉搜索树。
            / \   / \
           1   3 4   7
应当如此理解：左子树中的`所有节点`均小于当前值，右子树中的`所有节点`均大于当前值。

<br/><br/>

### AC Code ###

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
 
/**
  * Method: Using inorder traversal and generate inorder value list
  * if the inorder list is a increasing sequence, return true
  * else return false
  *
  */
 
class Solution {
public:
    bool isValidBST(TreeNode* root) {
    
        // if root is null, means that there are no node in the tree
        if(root == nullptr)
            return true;
        
        // if root have not left and right child, return ture
        if(root->left == nullptr && root->right == nullptr)
            return true;
        
        // using inorder traversal and generating the inorder list
        inorderTraversal(root);
        
        // if the inorder list is not increasing, return false
        for(int i = 1; i < nodeVal.size(); ++i)
        {
            if(nodeVal[i] <= nodeVal[i - 1])
                return false;
        }
        
        // else return true
        return true;
    }
    
    
    // recursion function for inorder traversal
    void inorderTraversal(TreeNode *root)
    {
        if(root == nullptr)
            return;
        inorderTraversal(root->left);
        nodeVal.push_back(root->val);
        inorderTraversal(root->right);
    }
    
private:
    vector<int> nodeVal;
};
```

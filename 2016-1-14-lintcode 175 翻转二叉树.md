#lintcode 175 翻转二叉树

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/restore-ip-addresses/

##解题报告



##Source Code / C++

**非递归版本**
用一个queue来模拟递归的过程，实现非递归版本。

```C++
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */
class Solution {
public:
    /**
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    void invertBinaryTree(TreeNode *root) {
        // write your code here
        if( !root ) return;
        queue<TreeNode*> q;
        q.push(root);
        while( !q.empty()) {
            TreeNode* node = q.front();
            q.pop();
            TreeNode* tmp = node->left;
            node->left = node->right;
            node->right = tmp;
            if( node->right ) q.push(node->right);
            if( node->left ) q.push(node->left);
            
        }
        return;
        
    }
};

```

**递归版本**
```C++

/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */
class Solution {
public:
    /**
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    void invertBinaryTree(TreeNode *root) {
        // write your code here
        invert(root);
        return;
    }
    
    TreeNode* invert(TreeNode* root) {
        if( !root ) return NULL;
        TreeNode* tmp = root->left;
        root->left = invert(root->right);
        root->right = invert(tmp);
        return root;
    }
};
```
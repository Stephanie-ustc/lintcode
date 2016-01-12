#lintcode 469 等价二叉树

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/identical-binary-tree/

##解题报告

递归，判断二叉树等价问题

##Source Code / C++ 

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
     * @aaram a, b, the root of binary trees.
     * @return true if they are identical, or false.
     */
    bool isIdentical(TreeNode* a, TreeNode* b) {
        // Write your code here
        if(a == NULL && b == NULL) return true;
        if(!(a != NULL && b!=NULL)) return false;
        return judge(a, b);
    }
    
    bool judge(TreeNode* a, TreeNode* b) {
        if(a->val != b-> val)
            return false;
            
        bool flag = true;
        if(a->left != NULL && b->left != NULL) {
            flag = flag & judge(a->left, b->left);
        } else if( !(a->left == NULL && b->left == NULL) ) {
            return false;
        }
        
        if(a->right != NULL && b->right != NULL) {
            flag = flag & judge(a->right, b->right);
        } else if( !(a->right == NULL && b->right == NULL)) {
            return false;
        }
        return flag;
    }
};

```
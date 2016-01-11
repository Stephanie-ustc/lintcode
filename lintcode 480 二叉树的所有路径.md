#lintcode 480 二叉树的所有路径

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

** 题目 **

题目链接：http://www.lintcode.com/zh-cn/problem/binary-tree-paths/

** 解题报告 **

简单的DFS

** Source Code / C++ **

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
     * @param root the root of the binary tree
     * @return all root-to-leaf paths
     */
    
    vector<string> ret;
    vector<string> binaryTreePaths(TreeNode* root) {
        // Write your code here
        if(root == NULL) return ret;
        findPath(root, "");
        return ret;
    }
    void findPath(TreeNode* root, string path) {
        stringstream ss;
        ss << root->val;
        if(root->left == NULL &&  root->right == NULL) {
            path = path + ss.str();
            ret.push_back(path);
        }
    
        if(root->left != NULL) {
            findPath(root->left, path + ss.str() + "->");
        }
        if(root->right != NULL) {
            findPath(root->right, path + ss.str() + "->");
        }
    }
};

```
#lintcode 535 打劫房屋 III

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目：
在上次打劫完一条街道之后和一圈房屋之后，窃贼又发现了一个新的可以打劫的地方，但这次所有的房子组成的区域比较奇怪，聪明的窃贼考察地形之后，发现这次的地形是一颗二叉树。与前两次偷窃相似的是每个房子都存放着特定金额的钱。你面临的唯一约束条件是：相邻的房子装着相互联系的防盗系统，且当相邻的两个房子同一天被打劫时，该系统会自动报警。

算一算，如果今晚去打劫，你最多可以得到多少钱，当然在不触动报警装置的情况下。

 注意事项

这题是House Robber和House Robber II的扩展，只不过这次地形由直线和圈变成了二叉树

您在真实的面试中是否遇到过这个题？ Yes
样例
  3
 / \
2   3
 \   \ 
  3   1
窃贼最多能偷窃的金钱数是 3 + 3 + 1 = 7.

    3
   / \
  4   5
 / \   \ 
1   3   1
窃贼最多能偷窃的金钱数是 4 + 5 = 9.

##解题报告



##Source Code / C++ 

```C++

    //Source Code
 /**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * }
 */
class Solution {
public:
    /**
     * @param root: The root of binary tree.
     * @return: The maximum amount of money you can rob tonight
     */
    void maxMoney(TreeNode* root, int *withMe, int * withoutMe) {
        int wMeL, woMeL;
        int wMeR, woMeR;
        
        if(!root) return;
        
        wMeL = woMeL = wMeR = woMeR =0;
        maxMoney(root->left, &wMeL, &woMeL);
        maxMoney(root->right, &wMeR, &woMeR);
        
        *withMe = root->val + woMeL + woMeR;
        *withoutMe = max(wMeL, woMeL)+ max(wMeR, woMeR);
         
    }
    int houseRobber3(TreeNode* root) {
        // write your code here
        int withMe, withoutMe;
        withMe = withoutMe = 0;
        maxMoney(root, &withMe, &withoutMe);
        return max(withMe, withoutMe);
    }
};

```
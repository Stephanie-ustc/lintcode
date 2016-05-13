#lintcode 223 回文链表

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/palindrome-linked-list/

##解题报告

链表操作

##Source Code / C++
 
```C++

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    /**
     * @param head a ListNode
     * @return a boolean
     */
    bool isPalindrome(ListNode* head) {
        // Write your code here
        if( !head || !head->next ) return true;
        ListNode* slow = head, *fast = head;
        while(fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        ListNode* last = slow->next, *pre = head;
        while(last->next) {
            ListNode* tmp = last->next;
            last->next = tmp->next;
            tmp->next = slow->next;
            slow->next= tmp;
        }
        
        while(slow->next) {
            slow = slow->next;
            if(pre->val != slow->val) return false;
            pre = pre->next;
        }
        return true;
    }
};

```
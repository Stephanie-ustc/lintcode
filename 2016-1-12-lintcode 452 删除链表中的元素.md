#lintcode 452 删除链表中的元素

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/remove-linked-list-elements/

##解题报告

链表初步应用

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
     * @param val an integer
     * @return a ListNode
     */
    ListNode *removeElements(ListNode *head, int val) {
        // Write your code here
        if(head == NULL) return head;
        ListNode dummy(-1);
        ListNode* pre = &dummy;
        pre->next = head;
        ListNode* index = head;
        while(index != NULL) {
            if(index->val == val) {
                pre->next = index->next;
                index = index->next;
            } else {
                pre = pre->next;
                index= index->next;
            }
        }
        
        return dummy.next;
    }
};

```
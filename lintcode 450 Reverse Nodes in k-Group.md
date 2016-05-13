#lintcode 450 Reverse Nodes in k-Group

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/reverse-nodes-in-k-group/

##解题报告



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
     * @param k an integer
     * @return a ListNode
     */
    ListNode *reverseKGroup(ListNode *head, int k) {
        // Write your code here
        if(head == NULL || k == 1) return head;
        ListNode dummy(-1);
        dummy.next = head;
        ListNode* pre = &dummy;
        int cnt =0;
        while(head != NULL) {
            ++cnt;
            if( cnt%k ==0) {
                pre = reverse(pre, head->next);
                head = pre->next;
            } else {
                head = head->next;
            }
        }
        return dummy.next;
    }
    ListNode* reverse(ListNode* pre, ListNode* next) {
        ListNode* last = pre->next;
        ListNode* cur = last->next;
        while(cur != next) {
            last->next = cur->next;
            cur->next = pre->next;
            pre->next = cur;
            cur = last->next;
        }
        return last;
    }
};
```
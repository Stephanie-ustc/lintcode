#lintcode 451 两两交换链表中的节点

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/swap-nodes-in-pairs/

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
     * @return a ListNode
     */
    ListNode* swapPairs(ListNode* head) {
        // Write your code here
        if(head == NULL || head->next == NULL) return head;
        ListNode dummy(-1);
        dummy.next =head;
        ListNode* index = &dummy;
        ListNode* pre = index->next;
        ListNode* cur = pre->next;
        while(cur != NULL) {
            //swap
            index->next = cur;
            pre->next = cur->next;
            cur->next = pre;
            if(pre->next == NULL || pre->next->next == NULL) {
                break;
            }
            index = index->next->next;
            pre = index->next;
            cur = index->next->next;
        }
        
        return dummy.next;
    }
};

```
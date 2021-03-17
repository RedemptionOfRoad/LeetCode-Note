# 把两个数字相加
题目描述见力扣官网，此处省略。
解决方案：
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int cf = 0; //当前两个数相加的进位值
        ListNode* ret = new ListNode(0); //结果链表
        ListNode* cur = ret;
        ListNode *p1 = l1, *p2 = l2; 
        int temp;
        while(p1 != nullptr || p2 != nullptr) {
            int x = (p1 != nullptr) ? p1->val : 0;
            int y = (p2 != nullptr) ? p2->val : 0;
            int sum = x + y + cf;
            cf = sum / 10;
            cur->next = new ListNode(sum % 10);
            cur = cur->next;
            if(p1 != nullptr) p1 = p1->next;
            if(p2 != nullptr) p2 = p2->next;
            
        }
        if(cf > 0) {
            cur->next = new ListNode(cf);
        }
        return ret->next;
    }
};
```

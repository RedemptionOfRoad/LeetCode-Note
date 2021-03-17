# 把两个数字相加
题目描述见力扣官网，此处省略。
解决方案：此处的解决思路完全是按照力扣官网给出的，只不过用C++实现了一遍
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
**思路误区：**
1. 一开始准备在第一层循环中再写这么几种情况的循环分别进行处理：
    a. p1和p2都不为空；
    b. p1为空，p2不为空；
    c. p1不为空，p2为空。
  这种方法应该是可行的，但是相当麻烦。
 2. 最高位相加的进位放在第一层循环外进行处理，如果放在循环内处理显得繁琐，导致思路比较混乱

**从题解中学到的方法：**
1. 首先要考虑输入有哪些情况需要处理，本题有那么几种情况：
    a. 两个链表等长；
    b. 两个链表不等长，但没有空链表；
    c. 两个链表不等长，但有空链表存在。
  最直接的思路就是分别处理这些情况，实际上，可以把这几种情况都视为两个等长的情况进行处理，只需要假装把长度较短链表与长度较长链表对应位置的数据域都设置为0即可。
2. 取结点数据域“新奇的”写法
    ```
    int x = (p1 != nullptr) ? p1->val : 0;
    ```

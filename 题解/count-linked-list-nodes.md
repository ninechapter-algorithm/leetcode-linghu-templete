# 链表节点计数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/count-linked-list-nodes/?utm_source=sc-github-wzz)
 ## 题目描述
 计算链表中有多少个节点.
 ### 样例说明
 ```
样例  1:
	输入:  1->3->5->null
	输出: 3
	
	样例解释: 
	返回链表中结点个数，也就是链表的长度.

样例 2:
	输入:  null
	输出: 0
	
	样例解释: 
	空链表长度为0

```
 ### 参考代码
 简单模拟
```cpp
/**
 * Definition of ListNode
 * class ListNode {
 * public:
 *     int val;
 *     ListNode *next;
 *     ListNode(int val) {
 *         this->val = val;
 *         this->next = NULL;
 *     }
 * }
 */
class Solution {
public:
    /**
     * @param head the first node of linked list.
     * @return an integer
     */
    int countNodes(ListNode *head) {
        // Write your code here
        int cnt = 0;
        while (head != NULL) {
            cnt ++;
            head = head->next;
        }
        return cnt;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
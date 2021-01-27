# 在排序链表中插入一个节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/insert-node-in-sorted-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 在链表中插入一个节点。
 ### 样例说明
 **样例 1：**
```
输入：head = 1->4->6->8->null, val = 5
输出：1->4->5->6->8->null
```
**样例 2：**
```
输入：head = 1->null, val = 2
输出：1->2->null
```
 ### 参考代码
 ----------------------------------------------------------
```python
"""
Definition of ListNode
class ListNode(object):

    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    # @param head, a ListNode
    # @param val, an integer
    # @return the head of new linked list
    def insertNode(self, head, val):
        # Write your code here
        dummy = ListNode(0, head)
        p = dummy
        while p.next and p.next.val < val:
            p = p.next
        node = ListNode(val, p.next)
        p.next = node
        return dummy.next
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
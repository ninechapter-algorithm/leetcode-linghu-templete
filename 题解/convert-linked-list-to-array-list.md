# 链表转数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-linked-list-to-array-list/?utm_source=sc-github-wzz)
 ## 题目描述
 将一个链表转换为一个数组。
 ### 样例说明
 **样例 1:**
```
输入: 1->2->3->null
输出: [1,2,3]
```
**样例 2:**
```
输入: 3->5->8->null
输出: [3,5,8]
```


 ### 参考代码
 ```python
"""
Definition of ListNode
class ListNode(object):

    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""
class Solution:
    """
    @param {ListNode} head the first node of the linked list.
    @return {int[]} an integer list
    """
    def toArrayList(self, head):
        # Write your code here
        r = []
        #遍历链表，并将每个节点的val存储在数组中
        while head is not None:
            r.append(head.val)
            head = head.next
        return r
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
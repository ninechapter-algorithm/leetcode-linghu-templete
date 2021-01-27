# 在O(1)时间复杂度删除链表节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/delete-node-in-the-middle-of-singly-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个单链表中的一个等待被删除的节点(非表头或表尾)。请在在 O(1) 时间复杂度删除该链表节点。
 ### 样例说明
 
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
    # @param node: the node in the list should be deleted
    # @return: nothing
    def deleteNode(self, node):
        # write your code here
        if node is None or node.next is None:
            return
        next = node.next;
        node.val = next.val
        node.next = next.next
        return
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
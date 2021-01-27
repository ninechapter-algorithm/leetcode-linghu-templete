# 向循环有序链表插入节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/insert-into-a-cyclic-sorted-list/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个来自已经排过序的循环链表的节点，写一个函数来将一个值插入到循环链表中，并且保持还是有序循环链表。给出的节点可以是链表中的任意一个单节点。返回插入后的新链表。
 ### 样例说明
 例1:
```
输入:
3->5->1
4
输出:
5->1->3->4
```

例2:
```
输入:
2->2->2
3
输出:
3->2->2->2
```

 ### 参考代码
 由于已经是排序好的链表。
所以只需顺序扫描一遍链表即可。
需要注意的是，若为最大或是最小，需要额外判断。
```python
"""
Definition of ListNode
class ListNode(object):

    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""
class Solution:
    # @param {ListNode} node a list node in the list
    # @param {int} x an integer
    # @return {ListNode} the inserted new list node
    def insert(self, node, x):
        # Write your code here
        if node is None:
            node = ListNode(x)
            node.next = node
            return node

        p = node
        prev = None
        while True:
            prev = p
            p = p.next
            if x <= p.val and x >= prev.val:
                break

            if (prev.val > p.val) and (x < p.val or x > prev.val):
                break

            if p is node:
                break

        newNode = ListNode(x)
        newNode.next = p
        prev.next = newNode
        return newNode
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
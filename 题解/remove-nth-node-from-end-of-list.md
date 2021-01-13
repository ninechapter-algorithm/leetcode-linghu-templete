# 删除链表中倒数第n个节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-nth-node-from-end-of-list/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">给定一个链表，删除链表中倒数第n个节点，返回链表的头节点。</span><br></p><p><br></p>
 ### 样例说明
 
 ### 参考代码
 Given a linked list, remove the nth node from the end of list and return its head.

For example,

   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:
Given n will always be valid.
Try to do this in one pass.

先让快指针走n步，然后快慢一起走，走到头的时候慢指针指向的点删掉。
```python
class Solution(object):
    '''
    题意：删除链表中倒数第n个结点，尽量只扫描一遍。
    使用两个指针扫描，当第一个指针扫描到第N个结点后，
    第二个指针从表头与第一个指针同时向后移动，
    当第一个指针指向空节点时，另一个指针就指向倒数第n个结点了       
    '''
    def removeNthFromEnd(self, head, n):
        res = ListNode(0)
        res.next = head
        tmp = res
        for i in range(0, n):
            head = head.next
        while head != None:
            head = head.next
            tmp = tmp.next
        tmp.next = tmp.next.next
        return res.next
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
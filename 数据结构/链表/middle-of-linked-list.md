# 链表的中点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/middle-of-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 找链表的中点。
 ### 样例说明
 **样例 1:**
```
输入:  1->2->3
输出: 2	
样例解释: 返回中间节点的值
```
**样例 2:**
```
输入:  1->2
输出: 1	
样例解释: 如果长度是偶数，则返回中间偏左的节点的值。	
```	
 ### 参考代码
 这里使用快慢指针的方法来寻找终点。
可以确保时间复杂度是 O(n/2)

快指针每次两步，慢指针每次一步。
快指针到尾的时候，慢指针就是中点。
```python
"""
Definition of ListNode
class ListNode(object):

    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    # @param head: the head of linked list.
    # @return: a middle node of the linked list
    def middleNode(self, head):
        # Write your code here
        if head is None:
            return None
        slow = head
        fast = slow.next
        while fast is not None and fast.next is not None:
            slow = slow.next
            fast = fast.next.next

        return slow
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
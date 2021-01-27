# 翻转链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reverse-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>翻转一个链表</p>
 ### 样例说明
 **样例 1:**

```
输入: 1->2->3->null
输出: 3->2->1->null
```

**样例 2:**

```
输入: 1->2->3->4->null
输出: 4->3->2->1->null
```
 ### 参考代码
 http://www.lintcode.com/zh-cn/problem/reverse-linked-list/
```python
class Solution:

    def reverse(self, head):
        #curt表示前继节点
        curt = None
        while head != None:
            #temp记录下一个节点，head是当前节点
            temp = head.next
            head.next = curt
            curt = head
            head = temp
        return curt
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
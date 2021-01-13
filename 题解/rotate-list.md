# 旋转链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rotate-list/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">给定一个链表，</span><span style="line-height: 1.42857143;">旋转链表，使得每个节点向右移动</span><span style="line-height: 1.42857143;">k个位置，其中k是一个非负数</span></p>
 ### 样例说明
 **样例 1:**
```
输入：1->2->3->4->5  k = 2
输出：4->5->1->2->3
```

**样例 2:**
```
输入：3->2->1  k = 1
输出：1->3->2
```
 ### 参考代码
 Given a list, rotate the list to the right by k places, where k is non-negative.

For example:
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.
```java
public class Solution {
    private int getLength(ListNode head) {
        int length = 0;
        while (head != null) {
            length ++;
            head = head.next;
        }
        return length;
    }
    
    public ListNode rotateRight(ListNode head, int n) {
        if (head == null) {
            return null;
        }
        
        int length = getLength(head);
        n = n % length;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        
        ListNode tail = dummy;
        for (int i = 0; i < n; i++) {
            head = head.next;
        }
        
        while (head.next != null) {
            tail = tail.next;
            head = head.next;
        }
        
        head.next = dummy.next;
        dummy.next = tail.next;
        tail.next = null;
        return dummy.next;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 删除排序链表中的重复数字 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-duplicates-from-sorted-list-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个排序链表，删除所有重复的元素只留下原链表中没有重复的元素。

 ### 样例说明
 ***样例 1***
```
输入 : 1->2->3->3->4->4->5->null
输出 : 1->2->5->null
```

***样例 2***
```
输入 : 1->1->1->2->3->null
输出 : 2->3->null
```
 ### 参考代码
 Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.
```java

public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null)
            return head;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;

        while (head.next != null && head.next.next != null) {
            if (head.next.val == head.next.next.val) {
                int val = head.next.val;
                while (head.next != null && head.next.val == val) {
                    head.next = head.next.next;
                }            
            } else {
                head = head.next;
            }
        }
        
        return dummy.next;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
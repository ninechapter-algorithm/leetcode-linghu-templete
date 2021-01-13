# 删除排序链表中的重复元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-duplicates-from-sorted-list/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个排序链表，删除所有重复的元素每个元素只留下一个。
 ### 样例说明
 ```
样例 1:
	输入:  null
	输出: null


样例 2:
	输入: 1->1->2->null
	输出: 1->2->null

样例 3:
	输入: 1->1->2->3->3->null
	输出: 1->2->3->null


```
 ### 参考代码
 Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.

跳过相同的元素，指向再后一个元素。
```java
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }

        ListNode node = head;
        while (node.next != null) {
            if (node.val == node.next.val) {
                node.next = node.next.next;
            } else {
                node = node.next;
            }
        }
        return head;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
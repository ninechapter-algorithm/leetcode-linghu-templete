# 两两交换链表中的节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/swap-nodes-in-pairs/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个链表，两两交换其中的节点，然后返回交换后的链表。
 ### 样例说明
 **样例 1：**
```
输入：1->2->3->4->null
输出：2->1->4->3->null
```
**样例 2：**
```
输入：5->null
输出：5->null
```
 ### 参考代码
 Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param head a ListNode
     * @return a ListNode
     */
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        head = dummy;
        while (head.next != null && head.next.next != null) {
            ListNode n1 = head.next, n2 = head.next.next;
            // head->n1->n2->...
            // => head->n2->n1->...
            head.next = n2;
            n1.next = n2.next;
            n2.next = n1;
            
            // move to next pair
            head = n1;
        }
        
        return dummy.next;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
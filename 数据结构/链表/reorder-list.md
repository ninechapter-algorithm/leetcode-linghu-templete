# 重排链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reorder-list/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个单链表L: *L*<sub>0</sub>→*L*<sub>1</sub>→…→*L*<sub>n-1</sub>→*L*<sub>n</sub>,

重新排列后为：*L*<sub>0</sub>→*L*<sub>n</sub>→*L*<sub>1</sub>→*L*<sub>n-1</sub>→*L*<sub>2</sub>→*L*<sub>n-2</sub>→…

必须在不改变节点值的情况下进行原地操作。
 ### 样例说明
 ```
样例 1:
	输入: 1->2->3->4->null
	输出: 1->4->2->3->null

样例 2:
	输入: 1->2->3->4->5->null
	输出: 1->5->2->4->3->null
	
```



 ### 参考代码
 Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You must do this in-place without altering the nodes' values.

For example,
Given {1,2,3,4}, reorder it to {1,4,2,3}.

先找到中点，然后把后半段倒过来，然后前后交替合并。
```java
public class Solution {
    private ListNode reverse(ListNode head) {
        ListNode newHead = null;
        while (head != null) {
            ListNode temp = head.next;
            head.next = newHead;
            newHead = head;
            head = temp;
        }
        return newHead;
    }

    private void merge(ListNode head1, ListNode head2) {
        int index = 0;
        ListNode dummy = new ListNode(0);
        while (head1 != null && head2 != null) {
            if (index % 2 == 0) {
                dummy.next = head1;
                head1 = head1.next;
            } else {
                dummy.next = head2;
                head2 = head2.next;
            }
            dummy = dummy.next;
            index ++;
        }
        if (head1 != null) {
            dummy.next = head1;
        } else {
            dummy.next = head2;
        }
    }

    private ListNode findMiddle(ListNode head) {
        ListNode slow = head, fast = head.next;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }

    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }

        ListNode mid = findMiddle(head);
        ListNode tail = reverse(mid.next);
        mid.next = null;

        merge(head, tail);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 链表倒数第n个节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/nth-to-last-node-in-list/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>找到单链表倒数第n个节点，保证链表中节点的最少数量为n。</p>
 ### 样例说明
 
 ### 参考代码
 两个指针，先让快指针走n步， 然后一起走，快指针到头的时候，慢指针就是倒数第n个。
```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    /**
     * @param head: The first node of linked list.
     * @param n: An integer.
     * @return: Nth to last node of a singly linked list. 
     */
    ListNode nthToLast(ListNode head, int n) {
        if (head == null || n < 1) {
            return null;
        }
	
        ListNode p1 = head;
        ListNode p2 = head;
        for (int j = 0; j < n - 1; ++j) {
            if (p2 == null) {
                return null;
            }
            p2 = p2.next;
        }
        while (p2.next != null) {   
            p1 = p1.next;   
            p2 = p2.next;
	    }
	    return p1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
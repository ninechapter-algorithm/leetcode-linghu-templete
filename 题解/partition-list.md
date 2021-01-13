# 链表划分
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/partition-list/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个单链表和数值x，划分链表使得所有小于x的节点排在大于等于x的节点之前。</p><p>你应该保留两部分内链表节点原有的相对顺序。</p><p><br></p>
 ### 样例说明
 **样例  1:**

```
输入: list = null, x = 0
输出: null	
样例解释: 空链表本身满足要求
```

**样例 2:**

```
输入: list = 1->4->3->2->5->2->null, x = 3
输出: 1->2->2->4->3->5->null	
样例解释: 要保持原有的相对顺序。
```

 ### 参考代码
 Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given 1->4->3->2->5->2 and x = 3,
return 1->2->2->4->3->5.

双指针方法，用两个指针将两个部分分别串起来。最后在将两个部分拼接起来。
left指针用来串起来所有小于x的结点，
right指针用来串起来所有大于等于x的结点。
得到两个链表，一个是小于x的，一个是大于等于x的，做一个拼接即可。
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode partition(ListNode head, int x) {
        if (head == null) {
            return null;
        }
        
        ListNode leftDummy = new ListNode(0);
        ListNode rightDummy = new ListNode(0);
        ListNode left = leftDummy, right = rightDummy;
        
        while (head != null) {
            if (head.val < x) {
                left.next = head;
                left = head;
            } else {
                right.next = head;
                right = head;
            }
            head = head.next;
        }
        
        right.next = null;
        left.next = rightDummy.next;
        return leftDummy.next;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 交换链表当中两个节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/swap-two-nodes-in-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个链表以及两个权值`v1`和`v2`，交换链表中权值为`v1`和`v2`的这两个节点。保证链表中节点权值各不相同，如果没有找到对应节点，那么什么也不用做。
 ### 样例说明
 **样例 1:**

```
输入: 1->2->3->4->null, v1 = 2, v2 = 4
输出: 1->4->3->2->null
```

**样例 2:**

```
输入: 1->null, v1 = 2, v2 = 1
输出: 1->null
```
 ### 参考代码
 因为数据结构是单链表, 所以假设需要修改权值为 `v` 的节点的链接, 那么需要获取该节点的前驱节点.

我们需要定义一个虚节点, 作为链表头, 它不储存数据.

找到权值为 `v1` 和 `v2` 的节点之后, 分情况讨论:

- 如果二者本身是相邻的, 则一共需要修改三条边(即三个next关系) {a node} -> {v = v1} -> {v = v2} -> {a node}
- 如果二者是不相邻的, 则一共需要修改四条边 {a node} -> {v = v1} -> {some nodes} -> {v = v2} -> {a node} (假定v1在v2前)
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
     * @oaram v1 an integer
     * @param v2 an integer
     * @return a new head of singly-linked list
     */
    public ListNode swapNodes(ListNode head, int v1, int v2) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode node1Prev = null, node2Prev = null;
        ListNode cur = dummy;
        while (cur.next != null) {
            if (cur.next.val == v1) {
                node1Prev = cur;
            } else if (cur.next.val == v2) {
                node2Prev = cur;
            }
            cur = cur.next;
        }
        
        if (node1Prev == null || node2Prev == null) {
            return head;
        }
        
        if (node2Prev.next == node1Prev) {
            // make sure node2Prev.next is not node1Prev
            ListNode t = node1Prev;
            node1Prev = node2Prev;
            node2Prev = t;
        }
        
        ListNode node1 = node1Prev.next;
        ListNode node2 = node2Prev.next;
        ListNode node2Next = node2.next;
        if (node1Prev.next == node2Prev) {
            node1Prev.next = node2;
            node2.next = node1;
            node1.next = node2Next;
        } else {
            node1Prev.next = node2;
            node2.next = node1.next;
            
            node2Prev.next = node1;
            node1.next = node2Next;
        }
        
        return dummy.next;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
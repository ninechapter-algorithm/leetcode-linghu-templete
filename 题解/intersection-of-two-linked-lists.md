# 两个链表的交叉
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/intersection-of-two-linked-lists/?utm_source=sc-github-wzz)
 ## 题目描述
 请写一个程序，找到两个单链表最开始的交叉节点。
 ### 样例说明
 **样例 1：**
```
输入：
	A:          a1 → a2
	                   ↘
	                     c1 → c2 → c3
	                   ↗            
	B:     b1 → b2 → b3
输出：c1
解释：在节点 c1 开始交叉。
```

**样例 2:**

```
输入:
Intersected at 6
1->2->3->4->5->6->7->8->9->10->11->12->13->null
6->7->8->9->10->11->12->13->null
输出: Intersected at 6
解释：begin to intersect at node 6.
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param headA: the first list
     * @param headB: the second list
     * @return: a ListNode 
     */
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        
        // get the tail of list A.
        ListNode node = headA;
        while (node.next != null) {
            node = node.next;
        }
        node.next = headB;
        ListNode result = listCycleII(headA);
        node.next = null;
        return result;
    }
    
    private ListNode listCycleII(ListNode head) {
        ListNode slow = head, fast = head.next;
        
        while (slow != fast) {
            if (fast == null || fast.next == null) {
                return null;
            }
            
            slow = slow.next;
            fast = fast.next.next;
        }
        
        slow = head;
        fast = fast.next;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        
        return slow;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
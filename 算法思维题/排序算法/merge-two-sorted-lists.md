# 合并两个排序链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/merge-two-sorted-lists/?utm_source=sc-github-wzz)
 ## 题目描述
 将两个排序链表合并为一个新的排序链表
 ### 样例说明
 ```
样例 1:
	输入: list1 = null, list2 = 0->3->3->null
	输出: 0->3->3->null


样例2:
	输入:  list1 =  1->3->8->11->15->null, list2 = 2->null
	输出: 1->2->3->8->11->15->null

```

 ### 参考代码
 Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

与合并数组一个方法，两个指针往后走。
```java
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode lastNode = dummy;
        
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                lastNode.next = l1;
                l1 = l1.next;
            } else {
                lastNode.next = l2;
                l2 = l2.next;
            }
            lastNode = lastNode.next;
        }
        
        if (l1 != null) {
            lastNode.next = l1;
        } else {
            lastNode.next = l2;
        }
        
        return dummy.next;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
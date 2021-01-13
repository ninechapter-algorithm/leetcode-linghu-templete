# 删除链表中的元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-linked-list-elements/?utm_source=sc-github-wzz)
 ## 题目描述
 删除链表中等于给定值 `val` 的所有节点。
 ### 样例说明
 **样例 1：**
```
输入：head = 1->2->3->3->4->5->3->null, val = 3
输出：1->2->4->5->null
```
**样例 2：**
```
输入：head = 1->1->null, val = 1
输出：null
```

 ### 参考代码
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
     * @param val an integer
     * @return a ListNode
     */
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        
        while (head.next != null) {
            if (head.next.val == val) {
                head.next = head.next.next;
            } else {
                head = head.next;
            }
        }
        
        return dummy.next;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
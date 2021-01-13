# 在链表中找节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-node-in-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 在链表中找值为 value 的节点，如果没有的话，返回空(null)。
 ### 样例说明
 **样例 1:**
```
输入:  1->2->3 and value = 3
输出: 最后一个结点
```		
**样例 2:**
```
输入:  1->2->3 and value = 4
输出: null
```
 ### 参考代码
 简单模拟，复杂度O(n)
```java
/**
 * Definition for ListNode
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
    /**
     * @param head: the head of linked list.
     * @param val: an integer
     * @return: a linked node or null
     */
    public ListNode findNode(ListNode head, int val) { 
        for (ListNode node = head; node != null; node = node.next) {
            if (node.val == val) {
                return node;
            }
        }
        return null;
    }  
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
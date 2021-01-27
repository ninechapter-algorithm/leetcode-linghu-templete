# 翻转链表 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reverse-linked-list-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>翻转链表中第m个节点到第n个节点的部分</p>
 ### 样例说明
 例1:
```
输入: 1->2->3->4->5->NULL, m = 2 and n = 4, 
输出: 1->4->3->2->5->NULL.
```

例2:
```
输入: 1->2->3->4->NULL, m = 2 and n = 3, 
输出: 1->3->2->4->NULL.
```


 ### 参考代码
 1. 创建head.
2. 找到m的前一个节点-Pre
3. 记录Pre的下一个节点，它会是翻转链的尾部。
4. 翻转指定区间的链表，翻到最后一个节点时，把reverseTail.next指向它的next。这样就把翻转链表与之后
的链表接起来了。
5. 返回dummynode的下一个节点。
```java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 * }
 */
public class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (m >= n || head == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        
        for (int i = 1; i < m; i++) {
            if (head == null) {
                return null;
            }
            head = head.next;
        }
        
        ListNode premNode = head;
        ListNode mNode = head.next;
        ListNode nNode = mNode, postnNode = mNode.next;
        for (int i = m; i < n; i++) {
            if (postnNode == null) {
                return null;
            }
            ListNode temp = postnNode.next;
            postnNode.next = nNode;
            nNode = postnNode;
            postnNode = temp;
        }
        mNode.next = postnNode;
        premNode.next = nNode;
        
        return dummy.next;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
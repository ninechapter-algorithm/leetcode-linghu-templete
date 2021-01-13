# 回文链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/palindrome-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一种方式检查一个链表是否为回文链表。
 ### 样例说明
 **样例 1:**
```
输入: 1->2->1
输出: true
```

**样例 2:**
```
输入: 2->2->1
输出: false
```

 ### 参考代码
 ```java
// This code would destroy the original structure of the linked list.
// If you do not want to destroy the structure, you can reserve the second part back.
public class Solution {
    /**
     * @param head a ListNode
     * @return a boolean
     */
    public boolean isPalindrome(ListNode head) {
        if (head == null) {
            return true;
        }
        
        ListNode middle = findMiddle(head);
        middle.next = reverse(middle.next);
        
        ListNode p1 = head, p2 = middle.next;
        while (p1 != null && p2 != null && p1.val == p2.val) {
            p1 = p1.next;
            p2 = p2.next;
        }
        
        return p2 == null;
    }
    
    private ListNode findMiddle(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode slow = head, fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
    }
    
    private ListNode reverse(ListNode head) {
        ListNode prev = null;
        
        while (head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        
        return prev;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
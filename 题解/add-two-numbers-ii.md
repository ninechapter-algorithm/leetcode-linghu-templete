# 链表求和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/add-two-numbers-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 假定用链表表示两个数，其中每个节点仅包含一个数字。假设这两个数的数字`顺序`排列，请设计一种方法将两个数相加，并将其结果表现为链表的形式。

 ### 样例说明
 **样例 1:**
```
输入: 6->1->7   2->9->5
输出: 9->1->2
```

**样例 2:**
```
输入: 1->2->3   4->5->6
输出: 5->7->9
```


 ### 参考代码
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
    /**
     * @param l1: the first list
     * @param l2: the second list
     * @return: the sum list of l1 and l2 
     */
    public ListNode addLists2(ListNode l1, ListNode l2) {
        l1 = reverse(l1);
        l2 = reverse(l2);
        
        return reverse(addList1(l1, l2));
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
    
    private ListNode addList1(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        int carry = 0;
        
        while (l1 != null && l2 != null) {
            tail.next = new ListNode((l1.val + l2.val + carry) % 10);
            tail = tail.next;
            carry = (l1.val + l2.val + carry) / 10;
            
            l1 = l1.next;
            l2 = l2.next;
        }
        
        while (l1 != null) {
            tail.next = new ListNode((l1.val + carry) % 10);
            tail = tail.next;
            carry = (l1.val + carry) / 10;
            
            l1 = l1.next;
        }
        while (l2 != null) {
            tail.next = new ListNode((l2.val + carry) % 10);
            tail = tail.next;
            carry = (l2.val + carry) / 10;
            
            l2 = l2.next;
        }
        
        while (carry != 0) {
            tail.next = new ListNode(carry % 10);
            tail = tail.next;
            carry = carry / 10;
        }
        
        return dummy.next;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
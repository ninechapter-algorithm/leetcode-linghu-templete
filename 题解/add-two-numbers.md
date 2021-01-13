# 链表求和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/add-two-numbers/?utm_source=sc-github-wzz)
 ## 题目描述
 你有两个用链表代表的整数，其中每个节点包含一个数字。数字存储按照在原来整数中`相反`的顺序，使得第一个数字位于链表的开头。写出一个函数将两个整数相加，用链表形式返回和。
 ### 样例说明
 **样例 1:**

```
输入: 7->1->6->null, 5->9->2->null
输出: 2->1->9->null	
样例解释: 617 + 295 = 912, 912 转换成链表:  2->1->9->null
```

**样例 2:**

```
输入:  3->1->5->null, 5->9->2->null
输出: 8->0->8->null	
样例解释: 513 + 295 = 808, 808 转换成链表: 8->0->8->null
```
 ### 参考代码
 You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -&gt; 4 -&gt; 3) + (5 -&gt; 6 -&gt; 4)
Output: 7 -&gt; 0 -&gt; 8class Solution(object):<br><br>

从前到后模拟加法过程，用一个变量记录每次加法的进位。进位最开始为0，每次加法对应的节点数字相加再加上进位，对10取模得到结果对应位置，除以10得到新的进位。
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if(l1 == null && l2 == null) {
            return null;
        }
            
        ListNode head = new ListNode(0);
        ListNode point = head;
        int carry = 0;
        while(l1 != null && l2!=null){
            int sum = carry + l1.val + l2.val;
            point.next = new ListNode(sum % 10);
            carry = sum / 10;
            l1 = l1.next;
            l2 = l2.next;
            point = point.next;
        }
        
        while(l1 != null) {
            int sum =  carry + l1.val;
            point.next = new ListNode(sum % 10);
            carry = sum /10;
            l1 = l1.next;
            point = point.next;
        }
        
        while(l2 != null) {
            int sum =  carry + l2.val;
            point.next = new ListNode(sum % 10);
            carry = sum /10;
            l2 = l2.next;
            point = point.next;
        }
        
        if (carry != 0) {
            point.next = new ListNode(carry);
        }
        return head.next;
    }
}


// version: 高频题班
public class Solution {
    /**
     * @param l1: the first list
     * @param l2: the second list
     * @return: the sum list of l1 and l2
     */
    public ListNode addLists(ListNode l1, ListNode l2) {
        // write your code here
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;

        int carry = 0;
        for (ListNode i = l1, j = l2; i != null || j != null; ) {
            int sum = carry;
            sum += (i != null) ? i.val : 0;
            sum += (j != null) ? j.val : 0;

            tail.next = new ListNode(sum % 10);
            tail = tail.next;

            carry = sum / 10;
            i = (i == null) ? i : i.next;
            j = (j == null) ? j : j.next;
        }

        if (carry != 0) {
            tail.next = new ListNode(carry);
        }
        return dummy.next;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
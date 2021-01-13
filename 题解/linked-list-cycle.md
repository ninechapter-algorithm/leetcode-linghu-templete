# 带环链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/linked-list-cycle/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个链表，判断它是否有环。</p>
 ### 样例说明
 	```
	样例 1:
		输入: 21->10->4->5,  then tail connects to node index 1(value 10).
		输出: true
		
	样例 2:
		输入: 21->10->4->5->null
		输出: false
	
	```

 ### 参考代码
 Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?

快慢指针的经典题。
快指针每次走两步，慢指针一次走一步。
在慢指针进入环之后，快慢指针之间的距离每次缩小1，所以最终能相遇。
```java
public class Solution {
    public Boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }

        ListNode fast, slow;
        fast = head.next;
        slow = head;
        while (fast != slow) {
            if(fast==null || fast.next==null)
                return false;
            fast = fast.next.next;
            slow = slow.next;
        } 
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
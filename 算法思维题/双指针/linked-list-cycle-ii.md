# 带环链表 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/linked-list-cycle-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个链表，如果链表中存在环，则返回到链表中环的起始节点，如果没有环，返回null。</p>
 ### 样例说明
 **样例 1:**
```
输入：null,no cycle
输出：no cycle
解释：
链表为空，所以没有环存在。
```
**样例 2:**
```https://simplemde.com/markdown-guide
输入：-21->10->4->5，tail connects to node index 1
输出：10
解释：
最后一个节点5指向下标为1的节点，也就是10，所以环的入口为10。
```
 ### 参考代码
 Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Follow up:
Can you solve it without using extra space?

考点：
* 双指针链表判环

题解：
* 使用双指针判断链表中是否有环，慢指针每次走一步，快指针每次走两步，若链表中有环，则两指针必定相遇。
* 假设环的长度为l，环上入口距离链表头距离为a，两指针第一次相遇处距离环入口为b，则另一段环的长度为c=l-b，由于快指针走过的距离是慢指针的两倍，则有a+l+b=2*(a+b),又有l=b+c，可得a=c，故当判断有环时(slow==fast)时，移动头指针，同时移动慢指针，两指针相遇处即为环的入口。
```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next==null) {
            return null;
        }

        ListNode fast, slow;
        fast = head.next;			//快指针
        slow = head;				//慢指针
        while (fast != slow) {		//快慢指针相遇
            if(fast==null || fast.next==null)
                return null;
            fast = fast.next.next;
            slow = slow.next;
        } 
        
        while (head != slow.next) {  //同时移动head和慢指针
            head = head.next;
            slow = slow.next;
        }
        return head;				//两指针相遇处即为环的入口
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 无序链表的重复项删除
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-duplicates-from-unsorted-list/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一种方法，从无序链表中删除重复项。
 ### 样例说明
 **样例 1：**
```
输入：1->2->1->3->3->5->6->3->null
输出：1->2->3->5->6->null
```
**样例 2：**
```
输入：2->2->2->2->2->null
输出：2->null
```
 ### 参考代码
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
     * @param head: The first node of linked list.
     * @return: head node
     */
    public ListNode removeDuplicates(ListNode head) { 
        HashSet<Integer> hash = new HashSet<Integer>();
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        while (head.next != null) {
            if (hash.contains(head.next.val)) {
                head.next = head.next.next;
            } else {
                hash.add(head.next.val);
                head = head.next;
            }
        }
        
        return dummy.next;
    }  
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
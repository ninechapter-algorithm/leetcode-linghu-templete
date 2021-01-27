# 链表化数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-array-list-to-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 将一个数组变成链表
 ### 样例说明
 例1:
```
输入: [1,2,3,4], 
输出: 1->2->3->4->null.
```

例2:
```
输入: [1,2], 
输出: 1->2->null.
```

 ### 参考代码
 元素之间链起来即可
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
    /**
     * @param nums an integer array list
     * @return the first node of linked list
     */
    public ListNode toLinkedList(ArrayList<Integer> nums) {  
        // Write your code here
        if (nums.size() == 0)
            return null;
        ListNode head = null;
        ListNode p = null;
        for (Integer num : nums) {
            if (head == null) {
                head = new ListNode(num);
                p = head;
            } else {
                p.next = new ListNode(num);
                p = p.next;
            }
        }
        return head;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
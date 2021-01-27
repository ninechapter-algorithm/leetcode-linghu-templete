# 链表插入排序
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/insertion-sort-list/?utm_source=sc-github-wzz)
 ## 题目描述
 用插入排序对链表排序
 ### 样例说明
 ```
样例 1:
	输入: 0->null
	输出: 0->null


样例 2:
	输入:  1->3->2->0->null
	输出 :0->1->2->3->null
	

```

 ### 参考代码
 Sort a linked list using insertion sort.

与数组普通插入排序一样的做法。
```java
public class Solution {
    public ListNode insertionSortList(ListNode head) {
        ListNode dummy = new ListNode(0);
        // 这个dummy的作用是，把head开头的链表一个个的插入到dummy开头的链表里
        // 所以这里不需要dummy.next = head;

        while (head != null) {
            ListNode node = dummy;
            while (node.next != null && node.next.val < head.val) {
                node = node.next;
            }
            ListNode temp = head.next;
            head.next = node.next;
            node.next = head;
            head = temp;
        }

        return dummy.next;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
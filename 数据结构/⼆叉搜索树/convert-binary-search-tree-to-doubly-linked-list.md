# 将二叉查找树转换成双链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-binary-search-tree-to-doubly-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 将一个二叉查找树按照中序遍历转换成双向链表。
 ### 样例说明
 
 ### 参考代码
 ```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 * Definition for Doubly-ListNode.
 * public class DoublyListNode {
 *     int val;
 *     DoublyListNode next, prev;
 *     DoublyListNode(int val) {
 *         this.val = val;
 *         this.next = this.prev = null;
 *     }
 * }
 */ 
 
class ResultType {
    DoublyListNode first, last;
    
    public ResultType(DoublyListNode first, DoublyListNode last) {
        this.first = first;
        this.last = last;
    }
}

public class Solution {
    /**
     * @param root: The root of tree
     * @return: the head of doubly list node
     */
    public DoublyListNode bstToDoublyList(TreeNode root) {  
        if (root == null) {
            return null;
        }
        
        ResultType result = helper(root);
        return result.first;
    }
    
    //中序遍历函数 
    public ResultType helper(TreeNode root) {  
        if (root == null) {
            return null;
        }
        
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        DoublyListNode node = new DoublyListNode(root.val);
        
        ResultType result = new ResultType(null, null);
        
        //构造单链表
        if (left == null) {
            result.first = node;
        } else {
            result.first = left.first;
            left.last.next = node;
            node.prev = left.last;
        }
        
        if (right == null) {
            result.last = node;
        } else {
            result.last = right.last;
            right.first.prev = node;
            node.next = right.first;
        }
        
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
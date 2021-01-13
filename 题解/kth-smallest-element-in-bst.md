# Kth Smallest Element in BST
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/kth-smallest-element-in-bst/?utm_source=sc-github-wzz)
 ## 题目描述
 1799
 ### 样例说明
 1799
 ### 参考代码
 简单的使用 inorder traversal 就可以在 O(k + h) 的时间内得到结果。h 是树的高度
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    private int index, kth;
    
    public int kthSmallest(TreeNode root, int k) {
        index = 0;
        inorder(root, k);
        return kth;
    }
    
    private void inorder(TreeNode root, int k) {
        if (root == null) {
            return;
        }
        
        inorder(root.left, k);
        index++;
        if (index == k) {
            kth = root.val;
        }
        
        if (index < k) {
        	inorder(root.right, k);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
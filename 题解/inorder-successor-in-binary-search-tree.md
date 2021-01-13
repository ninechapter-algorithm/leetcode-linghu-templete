# 二叉树查找树中序后继
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/inorder-successor-in-binary-search-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个二叉查找树([什么是二叉查找树](http://www.lintcode.com/zh-cn/problem/validate-binary-search-tree/))，以及一个节点，求该节点的中序遍历后继，如果没有返回`null`
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode successor = null;
        while (root != null && root != p) {
            if (root.val > p.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }
        
        if (root == null) {
            return null;
        }
        
        if (root.right == null) {
            return successor;
        }
        
        root = root.right;
        while (root.left != null) {
            root = root.left;
        }
        
        return root;
    }
}

// version: 高频题班
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        // write your code here
        if (root == null || p == null) {
            return null;
        }

        if (root.val <= p.val) {
            return inorderSuccessor(root.right, p);
        } else {
            TreeNode left = inorderSuccessor(root.left, p);
            return (left != null) ? left : root;
        }
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
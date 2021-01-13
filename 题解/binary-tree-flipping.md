# 二叉树翻转
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-flipping/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉树，其中所有右节点要么是具有兄弟节点的叶节点(有一个共享相同父节点的左节点)或空白，将其倒置并将其转换为树，其中原来的右节点变为左叶子节点。返回新的根节点。
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
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the new root
     */
    public TreeNode upsideDownBinaryTree(TreeNode root) {
        // Write your code here     
        if (root == null || root.left == null) {
            return root;
        }
        TreeNode new_root = upsideDownBinaryTree(root.left);
        root.left.left = root.right;
        root.left.right = root;
        root.right = null;
        root.left = null;
        return new_root;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the new root
     */

    TreeNode dfs(TreeNode cur) {
        if (cur.left == null) {
            return cur;
        }
        TreeNode newRoot = dfs(cur.left);
        cur.left.right = cur;
        cur.left.left = cur.right;
        cur.left = null;            // important
        cur.right = null;
        return newRoot;
    }

    public TreeNode upsideDownBinaryTree(TreeNode root) {
        // Write your code here
        if (root == null) {
            return null;
        }
        return dfs(root);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
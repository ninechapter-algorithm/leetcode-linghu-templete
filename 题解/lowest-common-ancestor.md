# 最近公共祖先
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/lowest-common-ancestor/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一棵二叉树，找到两个节点的最近公共父节点(LCA)。</p><p>最近公共祖先是两个节点的公共的祖先节点且具有最大深度。</p>
 ### 样例说明
 
 ### 参考代码
 LCA
```java
Version : Divide & Conquer

public class Solution {
    // 在root为根的二叉树中找A,B的LCA:
    // 如果找到了就返回这个LCA
    // 如果只碰到A，就返回A
    // 如果只碰到B，就返回B
    // 如果都没有，就返回null
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode node1, TreeNode node2) {
        if (root == null || root == node1 || root == node2) {
            return root;
        }
        
        // Divide
        TreeNode left = lowestCommonAncestor(root.left, node1, node2);
        TreeNode right = lowestCommonAncestor(root.right, node1, node2);
        
        // Conquer
        if (left != null && right != null) {
            return root;
        } 
        if (left != null) {
            return left;
        }
        if (right != null) {
            return right;
        }
        return null;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
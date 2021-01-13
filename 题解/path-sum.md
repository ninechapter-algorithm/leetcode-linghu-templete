# 路径和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/path-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定二叉树和求和，确定树是否具有根到叶路径，使得沿路径的所有值相加等于给定的总和。
 ### 样例说明
 
 ### 参考代码
 使用深度搜索的方法，当搜索到叶子节点时，比较与目标和的值，若相同，则结果为真，若搜索完毕没有出现目标和，返回假
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
     * @param root: the tree
     * @param sum: the sum
     * @return:  if the tree has a root-to-leaf path 
     */
    public boolean pathSum(TreeNode root, int sum) {
        // Write your code here.
        if (root == null) return false;
        else if (root.val == sum && root.left == null && root.right == null) return true;
        else return pathSum(root.left, sum - root.val) || pathSum(root.right, sum - root.val);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
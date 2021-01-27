# 二叉树的最大路径和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-maximum-path-sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树，找出从根节点出发的路径中，和最大的一条。

这条路径可以在任何二叉树中的节点结束，但是必须包含至少一个点（也就是根了）。

 ### 样例说明
 **样例 1:**

```
输入: {1,2,3}
输出: 4
解释: 
    1
   / \
  2   3
1+3=4
```

**样例 2:**

```
输入: {1,-1,-1}
输出: 1
解释:
    1
   / \
  -1 -1 
```
 ### 参考代码
 如果从动态规划的角度思考, 可以是这样的:

- 状态: f[i] 表示从节点i往下走得到的最大路径和
- 状态转移方程: f[i] = max{f[lc[i]], f[rc[i]], 0} + val[i]

不过这道题目是二叉树, 比经典的数字三角形要简单, 无需记忆化/定义额外空间储存答案.

一次递归遍历整棵二叉树即可.
```java
public class Solution {
    /**
     * @param root the root of binary tree.
     * @return an integer
     */
    public int maxPathSum2(TreeNode root) {
        if (root == null) {
            return Integer.MIN_VALUE;
        }

        int left = maxPathSum2(root.left);
        int right = maxPathSum2(root.right);
        return root.val + Math.max(0, Math.max(left, right));
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
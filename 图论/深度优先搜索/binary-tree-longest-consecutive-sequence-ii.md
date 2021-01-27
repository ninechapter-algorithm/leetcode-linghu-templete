# 二叉树的最长连续子序列 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-longest-consecutive-sequence-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一棵二叉树，找到最长连续序列(单调且相邻节点值相差为1)路径的长度(节点数)。
路径起点跟终点可以为二叉树的任意节点。
 ### 样例说明
 **例1:**
```
输入:
{1,2,0,3}
输出:
4
解释:
    1
   / \
  2   0
 /
3
0-1-2-3
```

**例2:**
```
输入:
{3,2,2}
输出:
2
解释:
    3
   / \
  2   2
2-3
```


 ### 参考代码
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
class ResultType {
    public int max_length, max_down, max_up;
    ResultType(int len, int down, int up) {
        max_length = len;
        max_down = down;
        max_up = up;    
    }
}

public class Solution {
    /**
     * @param root the root of binary tree
     * @return the length of the longest consecutive sequence path
     */
    public int longestConsecutive2(TreeNode root) {
        // Write your code here
        return helper(root).max_length;
    }
    
    ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(0, 0, 0);
        }

        ResultType left = helper(root.left);
        ResultType right = helper(root.right);

        int down = 0, up = 0;
        if (root.left != null && root.left.val + 1 == root.val)
            down = Math.max(down, left.max_down + 1);

        if (root.left != null && root.left.val - 1 == root.val)
            up = Math.max(up, left.max_up + 1);

        if (root.right != null && root.right.val + 1 == root.val)
            down = Math.max(down, right.max_down + 1);

        if (root.right != null && root.right.val - 1 == root.val)
            up = Math.max(up, right.max_up + 1);

        int len = down + 1 + up;
        len = Math.max(len, Math.max(left.max_length, right.max_length));

        return new ResultType(len, down, up);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
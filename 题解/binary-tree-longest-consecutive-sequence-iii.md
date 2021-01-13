# 二叉树的最长连续子序列III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-longest-consecutive-sequence-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 这题是 `二叉树的最长连续子序列II` 的后续。
给出一棵 `k叉树`，找到最长连续序列路径的长度.
路径的开头跟结尾可以是树的任意节点。
 ### 样例说明
 例1:
```
输入:
5<6<7<>,5<>,8<>>,4<3<>,5<>,31<>>>
输出:
5
解释:
     5
   /   \
  6     4
 /|\   /|\
7 5 8 3 5 31

返回 5, // 3-4-5-6-7
```

例2:
```
输入:
1<>
输出:
1
```


 ### 参考代码
 从根结点开始dfs，每次搜相邻的相差1的结点，跟新即可
```java
/**
 * Definition for a multi tree node.
 * public class MultiTreeNode {
 *     int val;
 *     List<TreeNode> children;
 *     MultiTreeNode(int x) { val = x; }
 * }
 */
 class ResultType {
    public int max_len, max_down, max_up;
    ResultType(int len, int down, int up) {
        max_len = len;
        max_down = down;
        max_up = up;    
    }
}

public class Solution {
    /**
     * @param root the root of k-ary tree
     * @return the length of the longest consecutive sequence path
     */
    public int longestConsecutive3(MultiTreeNode root) {
        // Write your code here
        return helper(root).max_len;
    }
    
    ResultType helper(MultiTreeNode root) {
        if (root == null) {
            return new ResultType(0, 0, 0);
        }

        int down = 0, up = 0, max_len = 1;
        for (MultiTreeNode node : root.children) {
            ResultType type = helper(node);
            if (node.val + 1 == root.val)
                down = Math.max(down, type.max_down + 1);
            if (node.val - 1 == root.val)
                up = Math.max(up, type.max_up + 1);
            max_len = Math.max(max_len, type.max_len);
        }

        max_len = Math.max(down + 1 + up, max_len);
        return new ResultType(max_len, down, up);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
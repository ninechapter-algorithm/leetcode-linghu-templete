# 二叉树中的最大路径和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-maximum-path-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 <span style="line-height: 30px;"><font color="#000000">给出一棵二叉树，</font></span><font color="#000000"><span style="line-height: 30px;">寻找一条路径使其路径和最大，路径可以在任一节点中开始和结束（路径和为两个节点之间所在路径上的节点权值之和）</span></font><br>
 ### 样例说明
 ```
样例 1:
	输入:  给定一棵树（只有一个节点）:
	2
	输出：2
	
样例 2:
	输入:  给定一棵树：

      1
     / \
    2   3
		
	输出: 6

	
```
 ### 参考代码
 Given a binary tree, find the maximum path sum.&nbsp;<div>The path may start and end at any node in the tree.&nbsp;</div><div><br></div><div>For example:&nbsp;</div><div>Given the below binary tree,&nbsp;</div><div>&nbsp; 1&nbsp;</div><div>&nbsp;/ &nbsp;\&nbsp;</div><div>2 &nbsp; 3&nbsp;</div><div><span style="line-height: 1.42857143;">Return 6.</span><br></div><div><div><br></div><div>详细题解请见九章算法微博：<a href="http://weibo.com/3948019741/BBY7gwi89" target="_blank">http://weibo.com/3948019741/BBY7gwi89</a></div></div>

分治法。
需要考虑的是，子树中最大的路不一定必过根节点。所以要记录single Path的值。
见代码注释。
```java
public class Solution {
    private class ResultType {
        // singlePath: 从root往下走到任意点的最大路径，这条路径可以不包含任何点
        // maxPath: 从树中任意到任意点的最大路径，这条路径至少包含一个点
        int singlePath, maxPath; 
        ResultType(int singlePath, int maxPath) {
            this.singlePath = singlePath;
            this.maxPath = maxPath;
        }
    }

    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(0, Integer.MIN_VALUE);
        }
        // Divide
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);

        // Conquer
        int singlePath = Math.max(left.singlePath, right.singlePath) + root.val;
        singlePath = Math.max(singlePath, 0);

        int maxPath = Math.max(left.maxPath, right.maxPath);
        maxPath = Math.max(maxPath, left.singlePath + right.singlePath + root.val);

        return new ResultType(singlePath, maxPath);
    }

    public int maxPathSum(TreeNode root) {
        ResultType result = helper(root);
        return result.maxPath;
    }
}


// Version 2:
// SinglePath也定义为，至少包含一个点。
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: An integer.
     */
    private class ResultType {
        int singlePath, maxPath;
        ResultType(int singlePath, int maxPath) {
            this.singlePath = singlePath;
            this.maxPath = maxPath;
        }
    }

    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(Integer.MIN_VALUE, Integer.MIN_VALUE);
        }
        // Divide
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);

        // Conquer
        int singlePath =
            Math.max(0, Math.max(left.singlePath, right.singlePath)) + root.val;

        int maxPath = Math.max(left.maxPath, right.maxPath);
        maxPath = Math.max(maxPath,
                           Math.max(left.singlePath, 0) + 
                           Math.max(right.singlePath, 0) + root.val);

        return new ResultType(singlePath, maxPath);
    }

    public int maxPathSum(TreeNode root) {
        ResultType result = helper(root);
        return result.maxPath;
    }

}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
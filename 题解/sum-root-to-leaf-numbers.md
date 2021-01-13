# 根节点到叶节点求和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sum-root-to-leaf-numbers/?utm_source=sc-github-wzz)
 ## 题目描述
 给定仅包含来自`0-9`的数字的二叉树，每个根到叶路径可以表示数字。举个例子：root-to-leaf路径`1-> 2-> 3`，它代表数字`123`，找到所有根到叶的数的总和
 ### 样例说明
 **样例1**

```
输入: {1,2,3}
输出: 25
解释:
    1
   / \
  2   3
路径 1->2 表示数字 12.
路径 1->3 表示数字 13.
因此, sum = 12 + 13 = 25.
```

**样例2**

```
输入: {4,9,0,5,1}
输出: 1026
解释:
    4
   / \
  9   0
 / \
5   1
路径 4->9->5 表示数字 495.
路径 4->9->1 表示数字 491.
路径 4->0 表示数字 40.
因此, sum = 495 + 491 + 40 = 1026.
```
 ### 参考代码
 Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.&nbsp;<div>An example is the root-to-leaf path 1-&gt;2-&gt;3 which represents the number 123.&nbsp;
</div><div>Find the total sum of all root-to-leaf numbers.&nbsp;</div><div><br></div><div>For example,&nbsp;</div><div>&nbsp; 1&nbsp;</div><div>&nbsp;/ \&nbsp;</div><div>2 &nbsp;3&nbsp;</div><div><br></div><div>The root-to-leaf path 1-&gt;2 represents the number 12.&nbsp;</div><div>The root-to-leaf path 1-&gt;3 represents the number 13.&nbsp;</div><div><br></div><div>&nbsp;Return the sum = 12 + 13 = 25.</div><div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博：</span><font color="#666e70" face="Open Sans, Arial, sans-serif"><span style="line-height: 22.3999996185303px;"><a href="http://weibo.com/3948019741/BBFgh84Bn" target="_blank">http://weibo.com/3948019741/BBFgh84Bn</a></span></font><br></div>
```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public int sumNumbers(TreeNode root) {
        return dfs(root, 0);
    }

    private int dfs(TreeNode root, int prev){
        if(root == null) {
            return 0;
        }

        int sum = root.val + prev * 10;
        if(root.left == null && root.right == null) {
            return sum;
        }

        return dfs(root.left, sum) + dfs(root.right, sum);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
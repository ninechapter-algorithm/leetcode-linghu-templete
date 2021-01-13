# 最大二叉搜索子树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/largest-bst-subtree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一棵二叉树，找到是二叉搜索树的最大子树，最大子树定义为子树节点最多。
 ### 样例说明
 **样例 1:**
```
输入:
{10,5,15,1,8,#,7}
输出：
3

解释:
    10
    / \
   5  15
  / \   \ 
 1   8   7
二叉搜索树的最大子树为 :
   5
  / \
 1   8. 
返回子树大小3.
```

**样例 2:**
```
输入:
{1}
输出：
1
```
 ### 参考代码
 于每一个节点，都来验证其是否是BST，如果是的话，就统计节点的个数即可
```java
public class Solution {
    public class SuperNode {
        int ans;
        int small, large;
        boolean isBST;
        public SuperNode() {
            ans = 0;
            isBST = true;
            small = Integer.MAX_VALUE;
            large = -Integer.MAX_VALUE;
        }
    }
    public int largestBSTSubtree(TreeNode root) {
        return dfs(root).ans;
    }
    public SuperNode dfs(TreeNode node) {
        if (node == null) {
            return new SuperNode();
        }
        SuperNode now = new SuperNode();
        SuperNode left = dfs(node.left);
        SuperNode right = dfs(node.right);
        if (left.small < node.val) {
            now.small = left.small;
        } else {
            now.small = node.val;
        }
        now.large = Math.max(right.large,node.val);
        if (left.isBST && right.isBST && left.large <= node.val && right.small >= node.val) {
            now.ans = left.ans + right.ans +1;
            now.isBST = true;
        } else {
            now.ans=Math.max(left.ans,right.ans);
            now.isBST = false;
        }
        return now;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
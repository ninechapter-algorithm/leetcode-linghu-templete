# 左叶子的和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sum-of-left-leaves/?utm_source=sc-github-wzz)
 ## 题目描述
 找出给定二叉树中，所有左叶子的值之和。
 ### 样例说明
 **样例1**
```
输入：
{3,9,20,#,#,15,7}
输出：24

解释：这棵二叉树中，有两个左叶子结点，它们的值分别为9和15。因此返回24。
    3
   / \
  9  20
    /  \
   15   7
```

**样例 2:**
```
输入:
{1,#,2,#,3}
输出:
0

解释:
1
  \
    2
      \
       3
```
 ### 参考代码
 递归遍历二叉树的节点，判断当前节点是否有左儿子，进而判断左儿子是否为叶子节点。
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
public class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        if(root == null) {
            return 0;
        }
        int sum = 0;
        if(root.left != null)
        {
            TreeNode left = root.left;
            //如果左儿子为叶子节点
            if(left.left == null && left.right == null) {
                sum += left.val;
            }
            //否则继续递归遍历左子树
            else {
                sum += sumOfLeftLeaves(left);
            }
        }
        //递归遍历右子树
        if(root.right != null)
        {
            TreeNode right = root.right;
            sum += sumOfLeftLeaves(right);
        }
        return sum;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
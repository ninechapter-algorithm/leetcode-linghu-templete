# 恢复二叉搜索树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/recover-binary-search-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 在一棵二叉搜索树中, 只有两个节点是被交换的. 找到这些节点并交换, 如果没有节点被交换就返回原来的树的根节点.
 ### 样例说明
 **样例1**

```
输入： {4,5,2,1,3}
输出： {4,2,5,1,3}
解释：
给出的二叉搜索树：
    4
   / \
  5   2
 / \
1   3
返回：
    4
   / \
  2   5
 / \
1   3
```

**样例2**

```
输入： {1,2,5,4,3}
输出： {4,2,5,1,3}
解释：
给出的二叉搜索树：
    1
   / \
  2   5
 / \
4   3
返回：
    4
   / \
  2   5
 / \
1   3
```


 ### 参考代码
 Two elements of a binary search tree (BST) are swapped by mistake.&nbsp;<div>Recover the tree without changing its structure.&nbsp;</div><div><br></div><div>Note:&nbsp;</div><div>A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?<div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博：<a href="http://weibo.com/3948019741/BErgRBUCb" target="_blank">&nbsp;http://weibo.com/3948019741/BErgRBUCb</a></span><br></div></div>
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
    private TreeNode firstElement = null;
    private TreeNode secondElement = null;
    private TreeNode lastElement = new TreeNode(Integer.MIN_VALUE); 
    
    private void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        traverse(root.left);
        if (firstElement == null && root.val < lastElement.val) {
            firstElement = lastElement;
        }
        if (firstElement != null && root.val < lastElement.val) {
            secondElement = root;
        }
        lastElement = root;
        traverse(root.right);
    }
    
    public void recoverTree(TreeNode root) {
        // traverse and get two elements
        traverse(root);
        // swap
        int temp = firstElement.val;
        firstElement.val = secondElement.val;
        secondElement.val = temp;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
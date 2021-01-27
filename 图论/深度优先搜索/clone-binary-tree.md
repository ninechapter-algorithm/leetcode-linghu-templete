# 克隆二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/clone-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 深度复制一个二叉树。

给定一个二叉树，返回一个他的 **克隆品** 。
 ### 样例说明
 **样例1:**

```plain
输入: {1,2,3,4,5}
输出: {1,2,3,4,5}
解释：
样例中二叉树如下所示:
     1
   /  \
  2    3
 / \
4   5
```

**样例2:**

```plain
输入: {1,2,3}
输出: {1,2,3}
解释：
样例中二叉树如下所示:
   1
 /  \
2    3
```


 ### 参考代码
 这题采用dfs（深度优先搜索）的方法，从根节点开始，一步步的去复制这一颗树。每次去复制他的左节点和右节点即可。
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
     * @param root: The root of binary tree
     * @return root of new tree
     */
    public TreeNode cloneTree(TreeNode root) {
        // Write your code here
        if (root == null)
            return null; //搜到了空节点，直接返回
        TreeNode clone_root = new TreeNode(root.val); //创造当前深度的“根”
        clone_root.left = cloneTree(root.left);  //左子树
        clone_root.right = cloneTree(root.right); //右子树
        return clone_root;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 二叉查找树的中序后继
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/inorder-successor-in-bst/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉查找树([什么是二叉查找树](http://www.lintcode.com/zh-cn/problem/validate-binary-search-tree/))，以及一个节点，求该节点在中序遍历的后继，如果没有则返回`null`
 ### 样例说明
 **样例 1:**

```
输入: {1,#,2}, node with value 1
输出: 2
解释: 
  1
   \
    2
```

**样例 2:**

```
输入: {2,1,3}, node with value 1
输出: 2
解释: 
    2
   / \
  1   3
```

[二叉树的表示](https://www.lintcode.com/help/binary-tree-representation/)
 ### 参考代码
 首先要确定中序遍历的后继:

- 如果该节点有右子节点, 那么后继是其右子节点的子树中最左端的节点
- 如果该节点没有右子节点, 那么后继是离它最近的祖先, 该节点在这个祖先的左子树内.

使用循环实现:

- 查找该节点, 并在该过程中维护上述性质的祖先节点
- 查找到后, 如果该节点有右子节点, 则后继在其右子树内; 否则后继就是维护的那个祖先节点

使用递归实现:

- 如果根节点小于或等于要查找的节点, 直接进入右子树递归
- 如果根节点大于要查找的节点, 则暂存左子树递归查找的结果, 如果是 `null`, 则直接返回当前根节点; 反之返回左子树递归查找的结果.

在递归实现中, 暂存左子树递归查找的结果就相当于循环实现中维护的祖先节点.
```java
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode successor = null;
        while (root != null && root.val != p.val) {
            if (root.val > p.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }

        if (root == null) {
            return null;
        }

        if (root.right == null) {
            return successor;
        }

        root = root.right;
        while (root.left != null) {
            root = root.left;
        }

        return root;
    }
}

// version:高频题班
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null || p == null) {
            return null;
        }

        if (root.val <= p.val) {
            return inorderSuccessor(root.right, p);
        } else {
            TreeNode left = inorderSuccessor(root.left, p);
            return (left != null) ? left : root;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
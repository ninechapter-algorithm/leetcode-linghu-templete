# 把二叉搜索树转化成更大的树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-bst-to-greater-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定二叉搜索树(BST)，将其转换为更大的树，使原始BST上每个节点的值都更改为在原始树中大于等于该节点值的节点值之和(包括该节点)。
 ### 样例说明
 **样例1:**

```
输入 : {5,2,13}
              5
            /   \
           2     13
输出 : {18,20,13}
             18
            /   \
          20     13
```

**样例2:**

```
输入 : {5,3,15}
              5
            /   \
           3     15
输出 : {20,23,15}
             20
            /   \
          23     15
```


 ### 参考代码
 从右子树开始递归，每次加上右子树的和，再递归左子树即可。
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
     * @param root the root of binary tree
     * @return the new root
     */
    public int sum = 0;

    void helper(TreeNode root){
        if (root == null) {
            return;
        }
        if (root.right != null) {
            helper(root.right);
        }
        
        root.val = (sum += root.val);
        if (root.left != null) {
            helper(root.left);
        }
    }

    public TreeNode convertBST(TreeNode root) {
        // Write your code here
        helper(root);
        return root;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the new root
     */
    int sum = 0;

    void dfs(TreeNode cur) {
        if (cur == null) {
            return;
        }
        dfs(cur.right);
        sum += cur.val;
        cur.val = sum;
        dfs(cur.left);
    }

    public TreeNode convertBST(TreeNode root) {
        // Write your code here
        dfs(root);
        return root;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
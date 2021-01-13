# 二叉树的最大节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-maximum-node/?utm_source=sc-github-wzz)
 ## 题目描述
 在二叉树中寻找值最大的节点并返回。
 ### 样例说明
 **样例1:**

```
输入:
{1,-5,3,1,2,-4,-5}
输出: 3
说明:
这棵树如下所示：
     1
   /   \
 -5     3
 / \   /  \
1   2 -4  -5
```

**样例 2**

```plain
输入:
{10,-5,2,0,3,-4,-5}
输出: 10
说明:
这棵树如下所示：
     10
   /   \
 -5     2
 / \   /  \
0   3 -4  -5 
```


 ### 参考代码
 树上基本遍历
```java
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the max ndoe
     */
    public TreeNode maxNode(TreeNode root) {
        // Write your code here
        if (root == null)
            return root;

        TreeNode left = maxNode(root.left);
        TreeNode right = maxNode(root.right);
        return max(root, max(left, right));
    }

    TreeNode max(TreeNode a, TreeNode b) {
        if (a == null)
            return b;
        if (b == null)
            return a;
        if (a.val > b.val) {
            return a;
        }
        return b;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
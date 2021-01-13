# DFS Template
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/dfs-template/?utm_source=sc-github-wzz)
 ## 题目描述
 1736
 ### 样例说明
 1736
 ### 参考代码
 Binary Tree DFS template
```java
Template 1: Traverse

public class Solution {
    public void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        // do something with root
        traverse(root.left);
        // do something with root
        traverse(root.right);
        // do something with root
    }
}


Tempate 2: Divide & Conquer

public class Solution {
    public ResultType traversal(TreeNode root) {
        // null or leaf
        if (root == null) {
            // do something and return;
        }
        
        // Divide
        ResultType left = traversal(root.left);
        ResultType right = traversal(root.right);
        
        // Conquer
        ResultType result = Merge from left and right.
        return result;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
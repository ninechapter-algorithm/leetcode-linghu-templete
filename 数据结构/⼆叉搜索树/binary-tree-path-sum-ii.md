# 二叉树的路径和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-path-sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树和一个目标值，设计一个算法找到二叉树上的和为该目标值的所有路径。路径可以从任何节点出发和结束，但是需要是一条一直往下走的路线。也就是说，路径上的节点的层级是逐个递增的。
 ### 样例说明
 
 ### 参考代码
 ```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""
class Solution:
    # @param {TreeNode} root the root of binary tree
    # @param {int} target an integer
    # @return {int[][]} all valid paths
    def binaryTreePathSum2(self, root, target):
        # Write your code here
        result = []
        path = []
        if root is None:
            return result
        self.dfs(root, path, result, 0,  target)
        return result

    def dfs(self, root, path, result, l, target):
        if root is None:
            return
        path.append(root.val)
        tmp = target
        for i in xrange(l , -1, -1):
            tmp -= path[i]
            if tmp == 0:
                result.append(path[i:])

        self.dfs(root.left, path, result, l + 1, target)
        self.dfs(root.right, path, result, l + 1, target)

        path.pop()
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
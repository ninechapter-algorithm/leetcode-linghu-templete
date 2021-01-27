# 二叉树的路径和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-path-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉树，找出所有路径中各节点相加总和等于给定 `目标值` 的路径。

一个有效的路径，指的是从根节点到叶节点的路径。
 ### 样例说明
 **样例1:**

```plain
输入:
{1,2,4,2,3}
5
输出: [[1, 2, 2],[1, 4]]
说明:
这棵树如下图所示：
	     1
	    / \
	   2   4
	  / \
	 2   3
对于目标总和为5，很显然1 + 2 + 2 = 1 + 4 = 5
```

**样例2:**

```plain
输入:
{1,2,4,2,3}
3
输出: []
说明:
这棵树如下图所示：
	     1
	    / \
	   2   4
	  / \
	 2   3
注意到题目要求我们寻找从根节点到叶子节点的路径。
1 + 2 + 2 = 5, 1 + 2 + 3 = 6, 1 + 4 = 5 
这里没有合法的路径满足和等于3.
```


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
    def binaryTreePathSum(self, root, target):
        # Write your code here
        result = []
        path = []
        self.dfs(root, path, result, 0,  target)

        return result

    def dfs(self, root, path, result, len, target):
        if root is None:
            return
        path.append(root.val)
        len += root.val

        if root.left is None and root.right is None and len == target:
            result.append(path[:])

        self.dfs(root.left, path, result, len, target)
        self.dfs(root.right, path, result, len, target)

        path.pop()
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
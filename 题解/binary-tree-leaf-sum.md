# 二叉树叶子节点之和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-leaf-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 计算二叉树的叶子节点之和
 ### 样例说明
 **样例 1:**
```
输入：{1,2,3,4}
输出：7
解释：
    1
   / \
  2   3
 /
4
3+4=7
```
**样例 2:**
```
输入：{1,#,3}
输出：3
解释：
    1
      \
       3
```
 ### 参考代码
 递归求和即可
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
"""
class Solution:
    # @param {TreeNode} root the root of the binary tree
    # @return {int} an integer
    def leafSum(self, root):
        # Write your code here
        p = []
        self.dfs(root, p)
        return sum(p)
    def dfs(self, root, p):
        if root is None:
            return
        if root.left is None and root.right is None:
            p.append(root.val)
        self.dfs(root.left, p)
        self.dfs(root.right, p)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
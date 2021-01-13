# 二叉树的某层节点之和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-level-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一棵二叉树和一个整数代表树的某层深度。
计算二叉树的某层节点之和。
 ### 样例说明
 **样例 1:**
```
输入：{1,2,3,4,5,6,7,#,#,8,#,#,#,#,9},2
输出：5 
解释：
     1
   /   \
  2     3
 / \   / \
4   5 6   7
   /       \
  8         9
2+3=5
```
**样例 2:**
```
输入：{1,2,3,4,5,6,7,#,#,8,#,#,#,#,9},3
输出：22
解释：
     1
   /   \
  2     3
 / \   / \
4   5 6   7
   /       \
  8         9
4+5+6+7=22
```
 ### 参考代码
 递归遍历树，答案加上对应层的值即可
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
    # @param {int} level the depth of the target level
    # @return {int} an integer
    def levelSum(self, root, level):
        # Write your code here
        p = []
        self.dfs(root, p, 1, level)
        return sum(p)
    def dfs(self, root, p, dep, level):
        if root is None:
            return
        if dep == level:
            p.append(root.val)
            return

        self.dfs(root.left, p, dep+1, level)
        self.dfs(root.right, p, dep+1, level)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
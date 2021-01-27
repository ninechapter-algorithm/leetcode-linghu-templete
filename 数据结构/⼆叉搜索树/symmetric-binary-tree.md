# 对称二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/symmetric-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一颗二叉树，判断是否是对称二叉树
 ### 样例说明
 **样例 1:**
```
输入：{1,2,2,3,4,4,3}
输出：true
解释：

         1
        / \
       2   2
      / \ / \
      3 4 4 3

是一个对称的二叉树。
```
**样例 2:**
```
输入：{1,2,2,#,3,#,3}
输出：false
解释：

         1
        / \
        2  2
        \   \
         3   3

不是对称的二叉树。
```
 ### 参考代码
 递归地判断是否有对应结点
```python
1"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
"""
class Solution:
    """
    @param root, the root of binary tree.
    @return true if it is a mirror of itself, or false.
    """
    def help(self, p, q):
        if p == None and q == None: return True
        if p and q and p.val == q.val:
            return self.help(p.right, q.left) and self.help(p.left, q.right)
        return False
    
    def isSymmetric(self, root):
        # Write your code here
        if root:
            return self.help(root.left, root.right)
        return True
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
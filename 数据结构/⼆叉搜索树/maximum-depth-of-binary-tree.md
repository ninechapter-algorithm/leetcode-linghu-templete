# 二叉树的最大深度
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-depth-of-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的距离。
 ### 样例说明
 **样例  1:**

```
输入: tree = {}
输出: 0	
样例解释: 空树的深度是0。
```
**样例  2:**

```
输入: tree = {1,2,3,#,#,4,5}
输出: 3
样例解释: 树表示如下，深度是3
   1
  / \                
 2   3                
    / \                
   4   5
它将被序列化为{1,2,3,#,#,4,5}
```

 ### 参考代码
 Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.<div><br></div><div>详细解答请至九章微博：<a href="http://weibo.com/3948019741/BBY7gwi89" target="_blank">http://weibo.com/3948019741/BBY7gwi89</a></div>

简单的树的遍历，点i为根的树高度，等于高度最大的子树的高度+1。
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
"""
class Solution:
    """
    @param root: The root of binary tree.
    @return: An integer
    """ 
    def maxDepth(self, root):
        if root is None:
            return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
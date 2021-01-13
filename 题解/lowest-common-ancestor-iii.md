# 最近公共祖先 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/lowest-common-ancestor-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树和二叉树中的两个节点，找到这两个节点的最近公共祖先LCA。

两个节点的最近公共祖先，是指两个节点的所有父亲节点中（包括这两个节点），离这两个节点最近的公共的节点。

返回 `null` 如果两个节点在这棵树上不存在最近公共祖先的话。
 ### 样例说明
 **样例1**

```
输入: 
{4, 3, 7, #, #, 5, 6}
3 5
5 6
6 7 
5 8
输出: 
4
7
7
null
解释:
  4
 / \
3   7
   / \
  5   6

LCA(3, 5) = 4
LCA(5, 6) = 7
LCA(6, 7) = 7
LCA(5, 8) = null

```

**样例2**

```
输入:
{1}
1 1
输出: 
1
说明：
这棵树只有一个值为1的节点
```

 ### 参考代码
 每次返回 是否在左子树中找到了节点A，是否在右子树中找到了节点B，以及是否已经找到了LCA，
这三个结果。然后分类讨论。如果已经在子树中找到了LCA,就直接return。否则，如果当前节点是
A且在子树中找到了B，或者当前节点是B且已经在子树中找到了A，就说明当前节点是LCA。
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
"""
import copy
class Solution:
    """
    @param {TreeNode} root The root of the binary tree.
    @param {TreeNode} A and {TreeNode} B two nodes
    @return Return the LCA of the two nodes.
    """ 
    def lowestCommonAncestor3(self, root, A, B):
        # write your code here
        a, b, lca = self.helper(root, A, B)
        if a and b:
            return lca
        else:
            return None

    def helper(self, root, A, B):
        if root is None:
            return False, False, None
            
        left_a, left_b, left_node = self.helper(root.left, A, B)
        right_a, right_b, right_node = self.helper(root.right, A, B)
        
        a = left_a or right_a or root == A
        b = left_b or right_b or root == B
        
        if root == A or root == B:
            return a, b, root

        if left_node is not None and right_node is not None:
            return a, b, root
        if left_node is not None:
            return a, b, left_node
        if right_node is not None:
            return a, b, right_node

        return a, b, None
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
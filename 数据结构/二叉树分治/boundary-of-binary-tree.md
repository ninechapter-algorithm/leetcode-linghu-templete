# 二叉树边界
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/boundary-of-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉树，从根开始返回其**逆时针**方向的边界值。边界包括左边界、叶和右边界，没有重复的节点。

**左边界**的定义为从根到**最左边**节点的路径。**右边界**的定义为从根到**最右边**的节点的路径。

如果根没有左子树或右子树，那么根本身就是最左边或者最右边的节点。注意，这个定义只适用于二叉树的根节点，而不适用于任何子树。

而当根有左子树时，最左边的节点是：你以有先访问左子节点的方式遍历二叉树时，第一个碰到的叶子节点。最右边的节点的定义类似，方向相反。


 ### 样例说明
 **样例 1:**

```
输入: {1,#,2,3,4}
输出: [1,3,4,2]
解释:
  1
   \
    2
   / \
  3   4 
  根没有左子树，所以根本身是左边界。
  叶节点为节点3和节点4。
  右边界是节点1 2 4。注意逆时针方向意味着你应该输出反向右边界。
  所以用逆时针顺序排列它们没有重复，我们得到[1,3,4,2]
```

**样例 2:**

```
输入: {1,2,3,4,5,6,#,#,#,7,8,9,10}
输出: [1,2,4,7,8,9,10,6,3]
解释: 
          1
     /          \
    2            3
   / \          / 
  4   5        6   
     / \      / \
    7   8    9  10  
  左边的边界是节点1 2 4。(4最左边的节点)
  叶节点是节点4 7 8 9 10。
  右边界是节点1 3 6 10。(10是最右边的节点)。
  所以逆时针顺序排列，我们得到[1,2,4,7,8,9,10,6,3]
```
 ### 参考代码
 面试中更加容易被面试官接受的版本。
虽然使用 DFS 但是没有使用任何的 Recursion。
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: a TreeNode
    @return: a list of integer
    """
    def boundaryOfBinaryTree(self, root):
        if root is None:
            return []
            
        left_boundary = self.find_left_boundary(root.left)
        leaves = self.find_leaves(root)
        right_boundary = self.find_right_boundary(root.right)
        
        if left_boundary and leaves and left_boundary[-1] == leaves[0]:
            leaves = leaves[1:]
        if leaves and right_boundary and leaves[-1] == right_boundary[-1]:
            leaves = leaves[:-1]
        return [root.val] + left_boundary + leaves + list(reversed(right_boundary))

    def find_leaves(self, root):
        stack = [root]
        leaves = []
        while stack:
            node = stack.pop()
            if not node.left and not node.right:
                leaves.append(node.val)
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        return leaves
        
    def find_left_boundary(self, root):
        left_boundary = []
        while root is not None:
            left_boundary.append(root.val)
            if root.left:
                root = root.left
            elif root.right:
                root = root.right
            else:
                break
        return left_boundary
        
    def find_right_boundary(self, root):
        right_boundary = []
        while root is not None:
            right_boundary.append(root.val)
            if root.right:
                root = root.right
            elif root.left:
                root = root.left
            else:
                break
        return right_boundary
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
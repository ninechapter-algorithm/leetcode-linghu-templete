# 平衡二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/balanced-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个二叉树,确定它是高度平衡的。对于这个问题,一棵高度平衡的二叉树的定义是：一棵二叉树中每个节点的两个子树的深度相差不会超过1。&nbsp;<br></p>
 ### 样例说明
 ```
样例  1:
	输入: tree = {1,2,3}
	输出: true
	
	样例解释:
	如下，是一个平衡的二叉树。
		  1  
		 / \                
		2  3

	
样例  2:
	输入: tree = {3,9,20,#,#,15,7}
	输出: true
	
	样例解释:
	如下，是一个平衡的二叉树。
		  3  
		 / \                
		9  20                
		  /  \                
		 15   7 

	
样例  2:
	输入: tree = {1,#,2,3,4}
	输出: false
	
	样例解释:
	如下，是一个不平衡的二叉树。1的左右子树高度差2
		  1  
		   \                
		   2                
		  /  \                
		 3   4
	
```

 ### 参考代码
 Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

在树上做一次DFS，计算以每个点为根的子树高度。
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
    @return: True if this Binary tree is Balanced, or false.
    """
    def isBalanced(self, root):
        balanced, _ = self.validate(root)
        return balanced
        
    def validate(self, root):
        if root is None:
            return True, 0
            
        balanced, leftHeight = self.validate(root.left)
        if not balanced:
            return False, 0
        balanced, rightHeight = self.validate(root.right)
        if not balanced:
            return False, 0
            
        return abs(leftHeight - rightHeight) <= 1, max(leftHeight, rightHeight) + 1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
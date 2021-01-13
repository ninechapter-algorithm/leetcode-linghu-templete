# 将二叉树拆成链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/flatten-binary-tree-to-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 将一棵二叉树按照前序遍历拆解成为一个 `假链表`。所谓的假链表是说，用二叉树的 *right* 指针，来表示链表中的 *next* 指针。
 ### 样例说明
 **样例 1：**
```
输入：{1,2,5,3,4,#,6}
输出：{1,#,2,#,3,#,4,#,5,#,6}
解释：
     1
    / \
   2   5
  / \   \
 3   4   6
 
1
\
 2
  \
   3
    \
     4
      \
       5
        \
         6
```
**样例 2：**
```
输入：{1}
输出：{1}
解释：
         1
         1
```

 ### 参考代码
 使用 Divide & Conquer
分治函数 return 这个 tree 的最后一个点。> 引用文本
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
    @param root: a TreeNode, the root of the binary tree
    @return: nothing
    """
    def flatten(self, root):
        self.flatten_and_return_last_node(root)
        
    # restructure and return last node in preorder
    def flatten_and_return_last_node(self, root):
        if root is None:
            return None
            
        left_last = self.flatten_and_return_last_node(root.left)
        right_last = self.flatten_and_return_last_node(root.right)
        
        # connect 
        if left_last is not None:
            left_last.right = root.right
            root.right = root.left
            root.left = None
            
        return right_last or left_last or root
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
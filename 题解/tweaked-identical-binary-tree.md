# 扭转后等价的二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/tweaked-identical-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 检查两棵二叉树是否在经过若干次扭转后可以等价。扭转的定义是，交换任意节点的左右子树。等价的定义是，两棵二叉树必须为相同的结构，并且对应位置上的节点的值要相等。
 ### 样例说明
 **样例 1:**
```
输入：{1,2,3,4}，{1,3,2,#,#,#,4}
输出：true
解释：
        1             1
       / \           / \
      2   3    和   3   2
     /                   \
    4                     4

是相同的。
```
**样例 2:**
```
输入：{1,2,3,4}，{1,3,2,4}
输出：false
解释：

        1             1
       / \           / \
      2   3    和   3   2
     /             /
    4             4

不一样。
```
 ### 参考代码
 判断该子树不交换左右子树和交换左右子树是否能与对应的子树一致，往上回溯即可
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
    @param a, b, the root of binary trees.
    @return true if they are tweaked identical, or false.
    """
    def isTweakedIdentical(self, a, b):
        # Write your code here
        if a == None and b == None: return True
        if a and b and a.val == b.val:
            return self.isTweakedIdentical(a.left, b.left) and \
                    self.isTweakedIdentical(a.right, b.right) or \
                    self.isTweakedIdentical(a.left, b.right) and \
                    self.isTweakedIdentical(a.right, b.left)
        return False
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 线段树的构造 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/segment-tree-build-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 线段树是一棵二叉树，他的每个节点包含了两个额外的属性`start`和`end`用于表示该节点所代表的区间。`start`和`end`都是整数，并按照如下的方式赋值:

- 根节点的 `start` 和 `end` 由 `build` 方法所给出。
- 对于节点 A 的左儿子，有 `start=A.left, end=(A.left + A.right) / 2`。
- 对于节点 A 的右儿子，有 `start=(A.left + A.right) / 2 + 1, end=A.right`。
- 如果 `start` 等于 `end`, 那么该节点是叶子节点，不再有左右儿子。

对于给定数组实现`build`方法, 线段树的每个节点储存区间最大值, 返回根节点.
 ### 样例说明
 ```
输入: [3,2,1,4]
解释: 
这颗线段树将会是
          [0,3](max=4)
          /          \
       [0,1]         [2,3]    
      (max=3)       (max=4)
      /   \          /    \    
   [0,0]  [1,1]    [2,2]  [3,3]
  (max=3)(max=2)  (max=1)(max=4)
 ### 参考代码
 模板题, 递归构造线段树即可. 注意内存要分配在堆上, 而不是栈上.

Python代码为Python2版本
```python
"""
Definition of SegmentTreeNode:
class SegmentTreeNode:
    def __init__(self, start, end, max):
        self.start, self.end, self.max = start, end, max
        self.left, self.right = None, None
"""

class Solution:	
    # @oaram A: a list of integer
    # @return: The root of Segment Tree
    def build(self, A):
        return self.buildTree(0, len(A)-1, A)

    def buildTree(self, start, end, A):
        if start > end:
            return None

        node = SegmentTreeNode(start, end, A[start])
        if start == end:
            return node

        mid = (start + end) / 2
        node.left = self.buildTree(start, mid, A)
        node.right = self.buildTree(mid + 1, end, A)
        if node.left is not None and node.left.max > node.max:
            node.max = node.left.max
        if node.right is not None and node.right.max > node.max:
            node.max = node.right.max
        return node
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 线段树的构造
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/segment-tree-build/?utm_source=sc-github-wzz)
 ## 题目描述
 线段树是一棵二叉树，他的每个节点包含了两个额外的属性`start`和`end`用于表示该节点所代表的区间。start和end都是整数，并按照如下的方式赋值:

- 根节点的 _start_ 和 _end_ 由 `build` 方法所给出。
- 对于节点 A 的左儿子，有 `start=A.start, end=(A.start + A.end) / 2`。
- 对于节点 A 的右儿子，有 `start=(A.start + A.end) / 2 + 1, end=A.end`。
- 如果 _start_ 等于 _end_, 那么该节点是叶子节点，不再有左右儿子。

实现一个 `build` 方法，接受 _start_ 和 _end_ 作为参数, 然后构造一个代表区间 `[start, end]` 的线段树，返回这棵线段树的根。
 ### 样例说明
 **样例 1:**
```
输入：[1,4]
输出："[1,4][1,2][3,4][1,1][2,2][3,3][4,4]"
解释：
	               [1,  4]
	             /        \
	      [1,  2]           [3, 4]
	      /     \           /     \
	   [1, 1]  [2, 2]     [3, 3]  [4, 4]
```
**样例 2:**
```
输入：[1,6]
输出："[1,6][1,3][4,6][1,2][3,3][4,5][6,6][1,1][2,2][4,4][5,5]"
解释：
	       [1,  6]
             /        \
      [1,  3]           [4,  6]
      /     \           /     \
   [1, 2]  [3,3]     [4, 5]   [6,6]
   /    \           /     \
[1,1]   [2,2]     [4,4]   [5,5]
```
 ### 参考代码
 考点：
* 线段树
* 二分

题解：递归过程按照左子树范围为(start, (start + end) / 2)，右子树范围为((start + end) / 2 + 1, end)建树即可。
```python
"""
Definition of SegmentTreeNode:
class SegmentTreeNode:
    def __init__(self, start, end):
        this.start, this.end = start, end
        this.left, this.right = None, None
"""

class Solution:	
    # @param start, end: Denote an segment / interval
    # @return: The root of Segment Tree
    def build(self, start, end):
        if start > end:
            return None
        root = SegmentTreeNode(start, end)
        if start == end:
            return root
        root.left = self.build(start, (start + end) / 2)
        root.right = self.build((start + end) / 2 + 1, end)
        return root
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 线段树的修改
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/segment-tree-modify/?utm_source=sc-github-wzz)
 ## 题目描述
 对于一棵 **最大线段树**, 每个节点包含一个额外的 `max` 属性，用于存储该节点所代表区间的最大值。

设计一个 `modify` 的方法，接受三个参数 `root`、 `index` 和 `value`。该方法将 _root_ 为根的线段树中 [_start_, _end_] = [_index_, _index_] 的节点修改为了新的 _value_ ，并确保在修改后，线段树的每个节点的 _max_ 属性仍然具有正确的值。
 ### 样例说明
 **样例 1:**
```
输入："[1,4,max=3][1,2,max=2][3,4,max=3][1,1,max=2][2,2,max=1][3,3,max=0][4,4,max=3]",2,4
输出："[1,4,max=4][1,2,max=4][3,4,max=3][1,1,max=2][2,2,max=4][3,3,max=0][4,4,max=3]"
解释：
线段树:

	                      [1, 4, max=3]
	                    /                \
	        [1, 2, max=2]                [3, 4, max=3]
	       /              \             /             \
	[1, 1, max=2], [2, 2, max=1], [3, 3, max=0], [4, 4, max=3]

如何调用modify(root, 2, 4), 可以得到:

	                      [1, 4, max=4]
	                    /                \
	        [1, 2, max=4]                [3, 4, max=3]
	       /              \             /             \
	[1, 1, max=2], [2, 2, max=4], [3, 3, max=0], [4, 4, max=3]
```


**样例 2:**
```
输入："[1,4,max=3][1,2,max=2][3,4,max=3][1,1,max=2][2,2,max=1][3,3,max=0][4,4,max=3]",4,0
输出："[1,4,max=4][1,2,max=4][3,4,max=0][1,1,max=2][2,2,max=4][3,3,max=0][4,4,max=0]"
解释：
线段树:

	                      [1, 4, max=3]
	                    /                \
	        [1, 2, max=2]                [3, 4, max=3]
	       /              \             /             \
	[1, 1, max=2], [2, 2, max=1], [3, 3, max=0], [4, 4, max=3]
如果调用modify(root, 4, 0), 可以得到:
	
	                      [1, 4, max=2]
	                    /                \
	        [1, 2, max=2]                [3, 4, max=0]
	       /              \             /             \
	[1, 1, max=2], [2, 2, max=1], [3, 3, max=0], [4, 4, max=0]
```
 ### 参考代码
 考点：
* 线段树

题解：按照区间自上向下查询区间，然后修改叶子节点，再自下向上合并修改各节点信息。
```python
"""
Definition of SegmentTreeNode:
class SegmentTreeNode:
    def __init__(self, start, end, max):
        this.start, this.end, this.max = start, end, max
        this.left, this.right = None, None
"""

class Solution:	
    """
    @param root, index, value: The root of segment tree and 
    @ change the node's value with [index, index] to the new given value
    @return: nothing
    """
    def modify(self, root, index, value):
        # write your code here
        if root is None:
            return

        if root.start == root.end:
            root.max = value
            return
    
        if root.left.end >= index:
            self.modify(root.left, index, value)
        else:
            self.modify(root.right, index, value)
        
        root.max = max(root.left.max, root.right.max)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
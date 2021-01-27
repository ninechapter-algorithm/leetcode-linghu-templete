# 线段树的查询
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/segment-tree-query/?utm_source=sc-github-wzz)
 ## 题目描述
 对于一个有n个数的整数数组，在对应的线段树中, 根节点所代表的区间为0-n-1, 每个节点有一个额外的属性`max`，值为该节点所代表的数组区间start到end内的最大值。

为SegmentTree设计一个 `query` 的方法，接受3个参数`root`, `start`和`end`，线段树root所代表的数组中子区间[start, end]内的最大值。
 ### 样例说明
 **样例 1:**
```
输入："[0,3,max=4][0,1,max=4][2,3,max=3][0,0,max=1][1,1,max=4][2,2,max=2][3,3,max=3]",1,2
输出：4
解释：
对于数组 [1, 4, 2, 3], 对应的线段树为 :

	                  [0, 3, max=4]
	                 /             \
	          [0,1,max=4]        [2,3,max=3]
	          /         \        /         \
	   [0,0,max=1] [1,1,max=4] [2,2,max=2], [3,3,max=3]
[1,2]区间最大值为4
```


**样例 2:**
```
输入："[0,3,max=4][0,1,max=4][2,3,max=3][0,0,max=1][1,1,max=4][2,2,max=2][3,3,max=3]",2,3
输出：3
解释：
对于数组 [1, 4, 2, 3], 对应的线段树为 :

	                  [0, 3, max=4]
	                 /             \
	          [0,1,max=4]        [2,3,max=3]
	          /         \        /         \
	   [0,0,max=1] [1,1,max=4] [2,2,max=2], [3,3,max=3]
[2,3]区间最大值为3
```
 ### 参考代码
 考点：
* 线段树

题解：
线段树为二叉树，如果查询区间位于当前区间之中，返回max值即可，如果超出范围，返回极小值即可，继续向左右搜索。
```python
"""
Definition of SegmentTreeNode:
class SegmentTreeNode:
    def __init__(self, start, end, max):
        this.start, this.end, this.max = start, end, max
        this.left, this.right = None, None
"""

class Solution:	
    # @param root, start, end: The root of segment tree and 
    #                          an segment / interval
    # @return: The maximum number in the interval [start, end]
    def query(self, root, start, end):
        # write your code here
        if root.start > end or root.end < start:
            return -0x7fffff
    
        if start <= root.start and root.end <= end:
            return root.max
        
        return max(self.query(root.left, start, end), \
                   self.query(root.right, start, end))
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 线段树查询 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/segment-tree-query-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 对于一个数组，我们可以对其建立一棵 `线段树`, 每个结点存储一个额外的值 `count` 来代表这个结点所指代的数组区间内的元素个数. (数组中并不一定每个位置上都有元素)

实现一个 `query` 的方法，该方法接受三个参数 `root`, `start` 和 `end`, 分别代表线段树的根节点和需要查询的区间，找到数组中在区间[*start*, *end*]内的元素个数。
 ### 样例说明
 **样例 1:**
```
输入："[0,3,count=3][0,1,count=1][2,3,count=2][0,0,count=1][1,1,count=0][2,2,count=1][3,3,count=1]",[[1, 1], [1, 2], [2, 3], [0, 2]]
输出：[0,1,2,2]
解释：
对应的线段树为：

	                     [0, 3, count=3]
	                     /             \
	          [0,1,count=1]             [2,3,count=2]
	          /         \               /            \
	   [0,0,count=1] [1,1,count=0] [2,2,count=1], [3,3,count=1]

Input : query(1,1), Output: 0

Input : query(1,2), Output: 1

Input : query(2,3), Output: 2

Input : query(0,2), Output: 2
```



**样例 2:**
```
输入："[0,3,count=3][0,1,count=1][2,3,count=2][0,0,count=1][1,1,count=0][2,2,count=0][3,3,count=1]",[[1, 1], [1, 2], [2, 3], [0, 2]]
输出：[0,0,1,1]
解释：
对应的线段树为：

	                     [0, 3, count=2]
	                     /             \
	          [0,1,count=1]             [2,3,count=1]
	          /         \               /            \
	   [0,0,count=1] [1,1,count=0] [2,2,count=0], [3,3,count=1]

Input : query(1,1), Output: 0

Input : query(1,2), Output: 0

Input : query(2,3), Output: 1

Input : query(0,2), Output: 1
```

 ### 参考代码
 考点：
* 线段树

题解：递归实现线段树自上向下的区间查询，自下向上的合并统计即可。
```python
"""
Definition of SegmentTreeNode:
class SegmentTreeNode:
    def __init__(self, start, end, count):
        this.start, this.end, this.count = start, end, count
        this.left, this.right = None, None
"""

class Solution:	
    # @param root, start, end: The root of segment tree and 
    #                          an segment / interval
    # @return: The count number in the interval [start, end] 
    def query(self, root, start, end):
        # write your code here
        if root is None:
            return 0

        if root.start > end or root.end < start:
            return 0
    
        if start <= root.start and root.end <= end:
            return root.count
        
        return self.query(root.left, start, end) + \
                   self.query(root.right, start, end)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
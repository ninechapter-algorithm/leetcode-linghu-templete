# 岛屿的个数II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/number-of-islands-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定 n, m, 分别代表一个二维矩阵的行数和列数, 并给定一个大小为 k 的二元数组A. 初始二维矩阵全0. 二元数组A内的k个元素代表k次操作, 设第i个元素为 `(A[i].x, A[i].y)`, 表示把二维矩阵中下标为A[i].x行A[i].y列的元素由海洋变为岛屿. 问在每次操作之后, 二维矩阵中岛屿的数量. 你需要返回一个大小为k的数组.
 ### 样例说明
 **样例 1:**

```
输入: n = 4, m = 5, A = [[1,1],[0,1],[3,3],[3,4]]
输出: [1,1,2,2]
解释: 
0.  00000
    00000
    00000
    00000
1.  00000
    01000
    00000
    00000
2.  01000
    01000
    00000
    00000
3.  01000
    01000
    00000
    00010
4.  01000
    01000
    00000
    00011
```

**样例 2:**

```
输入: n = 3, m = 3, A = [[0,0],[0,1],[2,2],[2,1]]
输出: [1,1,2,2]
```
 ### 参考代码
 定义一个矩阵记录地图状态, 还需要定义初始含 $n \times m$ 个集合的并查集, 以及一个计数器, 记录当前岛屿的个数.

对于每一次操作(x, y), 如果(x, y)的上下左右都是0, 那么计数器加一; 如果不全为0, 则:

1. 并查集查询其四周的1所属的集合, 假设它们属于 k 个不同的集合
2. 计数器减去 k-1
3. 将这 k 个集合, 连同 (x, y), 合并

并查集的实现可以利用Point结构体, 也可以将二维坐标转换成一维.
```python
"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""

DIRECTIONS = [(0, -1), (0, 1), (-1, 0), (1, 0)]

class Solution:
    """
    @param n: An integer
    @param m: An integer
    @param operators: an array of point
    @return: an integer array
    """
    def numIslands2(self, n, m, operators):
        results = []
        island = set()
        self.size = 0
        self.father = {}
        for operator in operators:
            x, y = operator.x, operator.y
            if (x, y) in island:
                results.append(self.size)
                continue
            
            island.add((x, y))
            self.father[(x, y)] = (x, y)
            self.size += 1
            for delta_x, delta_y in DIRECTIONS:
                x_ = x + delta_x
                y_ = y + delta_y
                if (x_, y_) in island:
                    self.union((x_, y_), (x, y))
                
            results.append(self.size)
            
        return results

    def union(self, point_a, point_b):
        root_a = self.find(point_a)
        root_b = self.find(point_b)
        if root_a != root_b:
            self.father[root_a] = root_b
            self.size -= 1
        
    def find(self, point):
        path = []
        while point != self.father[point]:
            path.append(point)
            point = self.father[point]
            
        for p in path:
            self.father[p] = point
            
        return point
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
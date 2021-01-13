# 螺旋矩阵
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/spiral-matrix/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个包含 *m* x *n* 个要素的矩阵，（*m* 行, *n* 列），按照螺旋顺序，返回该矩阵中的所有要素。
 ### 样例说明
 **样例 1:**
```
输入:[[ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ]]
输出: [1,2,3,6,9,8,7,4,5]
```

**样例 2**
```
输入:[[ 6,4,1 ], [ 7,8,9 ]]
输出: [6,4,1,9,8,7]
```
 ### 参考代码
 Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
You should return [1,2,3,6,9,8,7,4,5].
```python
class Solution:
    # @param {int[][]} matrix a matrix of m x n elements
    # @return {int[]} an integer array
    def spiralOrder(self, matrix):
        # Write your code here
        if matrix == []: return []
        up = 0; left = 0
        down = len(matrix)-1
        right = len(matrix[0])-1
        direct = 0  # 0: go right   1: go down  2: go left  3: go up
        res = []
        while True:
            if direct == 0:
                for i in range(left, right+1):
                    res.append(matrix[up][i])
                up += 1
            if direct == 1:
                for i in range(up, down+1):
                    res.append(matrix[i][right])
                right -= 1
            if direct == 2:
                for i in range(right, left-1, -1):
                    res.append(matrix[down][i])
                down -= 1
            if direct == 3:
                for i in range(down, up-1, -1):
                    res.append(matrix[i][left])
                left += 1
            if up > down or left > right: return res
            direct = (direct+1) % 4
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
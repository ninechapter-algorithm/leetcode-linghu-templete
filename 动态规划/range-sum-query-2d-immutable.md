# 平面范围求和 -不可变矩阵
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/range-sum-query-2d-immutable/?utm_source=sc-github-wzz)
 ## 题目描述
 给一 二维矩阵,计算由左上角 `(row1, col1)` 和右下角 `(row2, col2)` 划定的矩形内元素和.
 ### 样例说明
 **样例1**
```
输入：
[[3,0,1,4,2],[5,6,3,2,1],[1,2,0,1,5],[4,1,0,1,7],[1,0,3,0,5]]
sumRegion(2, 1, 4, 3)
sumRegion(1, 1, 2, 2)
sumRegion(1, 2, 2, 4)
输出：
8
11
12
解释：
给出矩阵
[
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]
sumRegion(2, 1, 4, 3) = 2 + 0 + 1 + 1 + 0 + 1 + 0 + 3 + 0 = 8
sumRegion(1, 1, 2, 2) = 6 + 3 + 2 + 0 = 11
sumRegion(1, 2, 2, 4) = 3 + 2 + 1 + 0 + 1 + 5 = 12
```
**样例2**
```
输入：
[[3,0],[5,6]]
sumRegion(0, 0, 0, 1)
sumRegion(0, 0, 1, 1)
输出：
3
14
解释：
给出矩阵
[
  [3, 0],
  [5, 6]
]
sumRegion(0, 0, 0, 1) = 3 + 0 = 3
sumRegion(0, 0, 1, 1) = 3 + 0 + 5 + 6 = 14
```
 ### 参考代码
 不妨设$dp[i][j]$表示$(0,0)$到$(i,j)$的子矩阵和。
转移方程为：$dp[i][j]=dp[i][j-1]+dp[i][j-1]-dp[i][j]+a[i][j]$
对于$(row_1,col_1)$到$(row_2,col_2)$的子矩阵和答案为：$dp[row_2+1][col_2+1]-dp[row_1][col_2+1]-dp[row_2+1][col_1]+dp[row_1][col_1]$
```python
class NumMatrix(object):

    # @param {int[][]} matrix a 2D matrix
    def __init__(self, matrix):
        # Write your code here

        if len(matrix) == 0 or len(matrix[0]) == 0:
            return 
        
        n = len(matrix)
        m = len(matrix[0])
        
        self.dp  = [[0] * (m + 1) for _ in range(n + 1)]
        for r in range(n):
            for c in range(m):
                self.dp[r + 1][c + 1] = self.dp[r + 1][c] + self.dp[r][c + 1] + \
                    matrix[r][c] - self.dp[r][c]

        
    # @param {int} row1 an integer
    # @param {int} col1 an integer
    # @param {int} row2 an integer
    # @param {int} row2 an integer
    # @return {int} the sum of region
    def sumRegion(self, row1, col1, row2, col2):
        # Write your code here
        return self.dp[row2 + 1][col2 + 1] - self.dp[row1][col2 + 1] - \
            self.dp[row2 + 1][col1] + self.dp[row1][col1]
        


# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
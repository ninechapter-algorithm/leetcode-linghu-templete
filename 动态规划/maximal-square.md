# 最大正方形
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximal-square/?utm_source=sc-github-wzz)
 ## 题目描述
 在一个二维01矩阵中找到全为1的最大正方形, 返回它的面积.
 ### 样例说明
 **样例 1:**

```
输入:
[
  [1, 0, 1, 0, 0],
  [1, 0, 1, 1, 1],
  [1, 1, 1, 1, 1],
  [1, 0, 0, 1, 0]
]
输出: 4
```

**样例 2:**

```
输入: 
[
  [0, 0, 0],
  [1, 1, 1]
]
输出: 1
```
 ### 参考代码
 ## 算法：dp

非常经典的dp。我们约定$dp[i][j] $ 代表以（i,j）为右下角最大正方形的边长。

* 设定初始边界状态，$dp[0][i]=dp[i][0]=0$
*  考虑状态的转移，我们发现，如果$matrix[i][j]=0$，那么此时，以这个点为右下角的最大正方形为0，即形成不了正方形。
* 若$matrix[i][j]=1$，我们考虑$dp[i-1][j],dp[i][j-1],dp[i-1][j-1]$，三者分别为以（i-1，j）为右下，以（i，j-1）为右下，以（i-1，j-1）为右下的最大正方形边长。
* 我们取三者的min+1，此时一定为合法的并且包含（i，j）最大的边长。即$dp[i][j] = min{dp[i-1][j-1], dp[i-1][j], dp[i][j-1]} + 1$
* 最后的$ans=max\{dp[i][j]\}^2$

## 复杂度分析

* 时间复杂度$O(n*m)$
* 空间复杂度$O(m)$
```python
class Solution:
    """
    @param matrix: a matrix of 0 and 1
    @return: an integer
    """
    def maxSquare(self, matrix):
        if not matrix or not matrix[0]:
            return 0
            
        n, m = len(matrix), len(matrix[0])
        
        # intialization
        f = [[0] * m, [0] * m]
        for i in range(m):
            f[0][i] = matrix[0][i]
            
        edge = max(matrix[0])
        for i in range(1, n):
            f[i % 2][0] = matrix[i][0]
            for j in range(1, m):
                if matrix[i][j]:
                    f[i % 2][j] = min(f[(i - 1) % 2][j], f[i % 2][j - 1], f[(i - 1) % 2][j - 1]) + 1
                else:
                    f[i % 2][j] = 0
            edge = max(edge, max(f[i % 2]))

        return edge * edge
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
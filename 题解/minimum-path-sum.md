# 最小路径和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-path-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">给定一个只含非负整数的m*n网格，找到一条从左上角到右下角的可以使数字和最小的路径。</span><br></p><p><br></p>
 ### 样例说明
 ```
样例 1:
	输入:  [[1,3,1],[1,5,1],[4,2,1]]
	输出: 7
	
	样例解释：
	路线为： 1 -> 3 -> 1 -> 1 -> 1。


样例 2:
	输入:  [[1,3,2]]
	输出:  6
	
	解释:  
	路线是： 1 -> 3 -> 2

```
 ### 参考代码
 Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Dp[i][j] 存储从（0， 0） 到（i, j）的最短路径。
Dp[i][j] = min(Dp[i-1][j]), Dp[i][j-1]) + grid[i][j];
```python
class Solution:
    """
    @param grid: a list of lists of integers.
    @return: An integer, minimizes the sum of all numbers along its path
    """
    def minPathSum(self, grid):
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if i == 0 and j > 0:
                    grid[i][j] += grid[i][j-1]
                elif j == 0 and i > 0:
                    grid[i][j] += grid[i-1][j]
                elif i > 0 and j > 0:
                    grid[i][j] += min(grid[i-1][j], grid[i][j-1])
        return grid[len(grid) - 1][len(grid[0]) - 1]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
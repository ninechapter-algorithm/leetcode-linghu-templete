# 不同的路径 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/unique-paths-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 "[不同的路径](http://www.lintcode.com/problem/unique-paths/ "不同的路径")" 的跟进问题：

现在考虑网格中有障碍物，那样将会有多少条不同的路径？

网格中的障碍和空位置分别用 1 和 0 来表示。
 ### 样例说明
 
 ### 参考代码
 Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.

[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
The total number of unique paths is 2.

Note: m and n will be at most 100.

Dp[i][j]表示从开始到（i，j）位置的路径数， Dp[i][j] = Dp[i-1][j] + Dp[i][j-1]
如果对应位置为 1，则是障碍，Dp[i][j] = 0;
```java
public class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null || obstacleGrid.length == 0 || obstacleGrid[0].length == 0) {
            return 0;
        }
        
        int n = obstacleGrid.length;
        int m = obstacleGrid[0].length;
        int[][] paths = new int[n][m];
        
        for (int i = 0; i < n; i++) {
            if (obstacleGrid[i][0] != 1) {
                paths[i][0] = 1;
            } else {
                break;
            }
        }
        
        for (int i = 0; i < m; i++) {
            if (obstacleGrid[0][i] != 1) {
                paths[0][i] = 1; 
            } else {
                break;
            }
        }
        
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                if (obstacleGrid[i][j] != 1) {
                    paths[i][j] = paths[i - 1][j] + paths[i][j - 1];
                } else {
                    paths[i][j] = 0;
                }
            }
        }
        
        return paths[n - 1][m - 1];
    }
}

// 方法二
public class Solution {
    /**
     * @param obstacleGrid: A list of lists of integers
     * @return: An integer
     */
    public int uniquePathsWithObstacles(int[][] A) {
        int m = A.length;
        if (m == 0) {
            return 0;
        }
        int n = A[0].length;
        if (n == 0) {
            return 0;
        }
        
        if (A[0][0] == 1 || A[m-1][n-1] == 1) {
            return 0;
        }
        
        int[][] f = new int[2][n];
        int i, j, old, now;
        now = 0;

        for (i = 0; i < m; ++i) {
            old = now;
            now = 1 - now;
            for (j = 0; j < n; ++j) {
                f[now][j] = 0;
                if (A[i][j] == 1) {
                    f[now][j] = 0;
                }
                else {
                    if (i == 0 && j == 0) {
                        f[now][j] = 1;
                    }
                    if (i > 0) {
                        f[now][j] += f[old][j];
                    }
                    if (j > 0) {
                        f[now][j] += f[now][j-1];
                    }
                }
            }
        }
        
        return f[now][n-1];
    }
}


// 记忆化搜索
// 九章硅谷求职算法集训营版本
public class Solution {
    /**
     * @param obstacleGrid: A list of lists of integers
     * @return: An integer
     */
     
    int[][] f;
    int[][] A;
    int m;
    int n;
    
    void calc(int i, int j) {
        if (f[i][j] != -1) {
            return;
        }
        
        if (A[i][j] == 1) {
            f[i][j] = 0;
            return;
        }
        
        if (i == 0 && j == 0) {
            f[i][j] = 1;
            return;
        }
        
        f[i][j] = 0;
        if (i > 0) {
            calc(i - 1, j);
            f[i][j] += f[i - 1][j];
        }
        
        if (j > 0) {
            calc(i, j - 1);
            f[i][j] += f[i][j - 1];
        }
    }
    
    public int uniquePathsWithObstacles(int[][] AA) {
        A = AA;
        m = A.length;
        if (m == 0) {
            return 0;
        }
        
        n = A[0].length;
        if (n == 0) {
            return 0;
        }
        
        int i, j;
        f = new int[m][n];
        for (i = 0; i < m; ++i) {
            for (j = 0; j < n; ++j) {
                f[i][j] = -1;
            }
        }
    
        calc(m - 1, n - 1);
        return f[m - 1][n - 1];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
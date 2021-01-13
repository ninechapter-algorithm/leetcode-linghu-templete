# 不同的路径
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/unique-paths/?utm_source=sc-github-wzz)
 ## 题目描述
 有一个机器人的位于一个 *m* × *n* 个网格左上角。

机器人每一时刻只能向下或者向右移动一步。机器人试图达到网格的右下角。

问有多少条不同的路径？
 ### 样例说明
 
 ### 参考代码
 A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?


Above is a 3 x 7 grid. How many possible unique paths are there?

Note: m and n will be at most 100.

解法1:
数学模型：在n-1 + m-1长度的序列中，有n-1个D，和m-1个R组成。
其中D表示向下，R表示向右。
因此满足组合数：C(n+m-2, n-1), 从n+m-2个位置中选n-1个位置放D的方案数。

解法2:
可以用Dp过程来求解：
Dp[i][j] 表示走到(i,j)的路径数，
考虑最后一步是从上往下走，还是从左往右走。
Dp[i][j] = Dp[i-1][j] + Dp[i][j-1];
```java
public class Solution {
    public int uniquePaths(int m, int n) {
        if (m == 0 || n == 0) {
            return 1;
        }
        
        int[][] sum = new int[m][n];
        for (int i = 0; i < m; i++) {
            sum[i][0] = 1;
        }
        for (int i = 0; i < n; i++) {
            sum[0][i] = 1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                sum[i][j] = sum[i - 1][j] + sum[i][j - 1];
            }
        }
        return sum[m - 1][n - 1];
    }
}

// 方法二
public class Solution {
    /**
     * @param n, m: positive integer (1 <= n ,m <= 100)
     * @return an integer
     */
    public int uniquePaths(int m, int n) {
        int[][] f = new int[m][n];
        int i, j;
        for (i = 0; i < m; ++i) {
            for (j = 0; j < n; ++j) {
                if (i == 0 || j == 0) {
                    f[i][j] = 1;
                }
                else {
                    f[i][j] = f[i-1][j] + f[i][j-1];
                }
            }
        }
        
        return f[m-1][n-1];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
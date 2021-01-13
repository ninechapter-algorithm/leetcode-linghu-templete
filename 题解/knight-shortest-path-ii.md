# 骑士的最短路径II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/knight-shortest-path-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 在一个 `n * m` 的棋盘中(二维矩阵中 0 表示空 1 表示有障碍物)，骑士的初始位置是 `(0, 0)` ，他想要达到 `(n - 1, m - 1)` 这个位置，骑士只能从左边走到右边。找出骑士到目标位置所需要走的最短路径并返回其长度，如果骑士无法达到则返回 `-1`.
 ### 样例说明
 例1:
```
输入:
[[0,0,0,0],[0,0,0,0],[0,0,0,0]]
输出:
3
解释:
[0,0]->[2,1]->[0,2]->[2,3]
```

例2:
```
输入:
[[0,1,0],[0,0,1],[0,0,0]]
输出:
-1
```



 ### 参考代码
 简单动态规划。
每个点都有至多4个前缀点，直接求最小值转移即可。
```java
public class Solution {
    /**
     * @param grid a chessboard included 0 and 1
     * @return the shortest path
     */
    public int shortestPath2(boolean[][] grid) {
        // Write your code here
        int n = grid.length;
        if (n == 0)
            return -1;
        int m = grid[0].length;
        if (m == 0)
            return -1;

        int[][] f = new int[n][m];
        for (int i = 0; i < n; ++i)
            for (int j = 0; j < m; ++j)
                f[i][j] = Integer.MAX_VALUE;

        f[0][0] = 0;
        for (int j = 1; j < m; ++j)
          for (int i = 0; i < n; ++i)
            if (!grid[i][j]) {
                if (i >= 1 && j >= 2 && f[i - 1][j - 2] != Integer.MAX_VALUE)
                    f[i][j] = Math.min(f[i][j], f[i - 1][j - 2] + 1);
                if (i + 1 < n && j >= 2 && f[i + 1][j - 2] != Integer.MAX_VALUE)
                    f[i][j] = Math.min(f[i][j], f[i + 1][j - 2] + 1);
                if (i >= 2 && j >= 1 && f[i - 2][j - 1] != Integer.MAX_VALUE)
                    f[i][j] = Math.min(f[i][j], f[i - 2][j - 1] + 1);
                if (i + 2 < n && j >= 1 && f[i + 2][j - 1] != Integer.MAX_VALUE)
                    f[i][j] = Math.min(f[i][j], f[i + 2][j - 1] + 1);
            }

        if (f[n - 1][m - 1] == Integer.MAX_VALUE)
            return -1;

        return f[n - 1][m - 1];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 丢鸡蛋II


 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/drop-eggs-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 有一个`n`层的建筑。如果一个鸡蛋从第`k`层及以上落下，它会碎掉。如果从低于这一层的任意层落下，都不会碎。
有`m`个鸡蛋，用最坏的情况下实验次数最少的方法去找到k, 返回最坏情况下所需的实验次数。
 ### 样例说明
 
 ### 参考代码
 动态规划。
dp[i][j]代表从有i个鸡蛋在第j层需要的最少次数。
转移方程为
dp[i][j]=min(dp[i][j],max(dp[i - 1][k - 1], dp[i][j - k]))
即每次在第k层碎了所转移到的状态，以及第k层没碎所转移到的状态
```java
public class Solution {
    /**
     * @param m the number of eggs
     * @param n the umber of floors
     * @return the number of drops in the worst case
     */
    public int dropEggs2(int m, int n) {
        // Write your code here
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 1; i <= m; ++i) {
            dp[i][1] = 1;
            dp[i][0] = 0;
        }
     
        for (int j = 1; j <= n; ++j)
            dp[1][j] = j;

        for (int i = 2; i <= m; ++i) {
            for (int j = 2; j <= n; ++j) {
                dp[i][j] = Integer.MAX_VALUE;
                for (int k = 1; k <= j; ++k) {
                    dp[i][j] = Math.min(dp[i][j],
                        1 + Math.max(dp[i - 1][k - 1], dp[i][j - k]));
                }
            }
        }

        return dp[m][n];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
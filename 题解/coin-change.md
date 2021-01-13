# 换硬币
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/coin-change/?utm_source=sc-github-wzz)
 ## 题目描述
 给出不同面额的硬币以及一个总金额. 写一个方法来计算给出的总金额可以换取的最少的硬币数量. 如果已有硬币的任意组合均无法与总金额面额相等, 那么返回 `-1`.
 ### 样例说明
 **样例1**
```
输入：
[1, 2, 5]
11
输出： 3
解释： 11 = 5 + 5 + 1
```
**样例2**
```
输入： 
[2]
3
输出： -1
```
 ### 参考代码
 这是一个典型的完全背包问题。
设dp[i][j]表示使用前i个硬币，总金额为j时需要的最少硬币数量。

$dp[i][j]=max(dp[i-1][j],dp[i-1][j-k*coin[i]]+k) \quad (0\leq k*coin[i] \leq j)$
```java
public class Solution {
    public int coinChange(int[] A, int M) {
        int[] f = new int[M + 1];
        int n = A.length;
        
        f[0] = 0;
        int i, j;
        for (i = 1; i <= M; ++i) {
            f[i] = -1;
            for (j = 0; j < n; ++j) {
                if (i >= A[j] && f[i - A[j]] != -1) {
                    if (f[i] == -1 || f[i - A[j]] + 1 < f[i]) {
                        f[i] = f[i - A[j]] + 1;
                    }
                }
            }
        }
        
        return f[M];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
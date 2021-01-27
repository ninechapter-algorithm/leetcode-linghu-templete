# 买卖股票的最佳时机 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/best-time-to-buy-and-sell-stock-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>假设你有一个数组，它的第i个元素是一支给定的股票在第i天的价格。<span style="line-height: 1.42857143;">设计一个算法来找到最大的利润。你最多可以完成两笔交易。</span></p>
 ### 样例说明
 ***样例 1***
```
输入 : [4,4,6,1,1,4,2,5]
输出 : 6
```
 ### 参考代码
 Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
```java
// 动态规划专题班版本
public class Solution {
    /**
     * @param prices: Given an integer array
     * @return: Maximum profit
     */
    public int maxProfit(int[] prices) {
        // write your code here
        int n = prices.length;
        if (n == 0) {
            return 0;
        }
        int [][]dp = new int[n + 1][5 + 1];
        
        for (int k = 1; k <= 5; k++) {
            dp[0][k] = Integer.MIN_VALUE;
        }
        dp[0][1] = 0;
        for (int i = 1; i <= n; i++) {
            // 手中未持有股票
            for (int j = 1; j <= 5; j += 2) {
                // 前一天也未持有
                dp[i][j] = dp[i - 1][j];
                if (j > 1 && i > 1 && dp[i - 1][j - 1] != Integer.MIN_VALUE) {
                    //                            前一天持有，今天卖了获利。
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - 1] + prices[i - 1] - prices[i - 2]);
                }
            }
            // 手中持有股票
            for (int j = 2; j <= 5; j += 2) {
                //前一天未持有，今天买进
                dp[i][j] = dp[i - 1][j - 1];
                if (i > 1 && dp[i - 1][j] != Integer.MIN_VALUE) {
                    //                            前一天持有了，计算今天的利润
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j] + prices[i - 1] - prices[i - 2]);
                }
            }
        }
        
        int res = 0;
        for (int j = 1; j <= 5; j += 2) {
            res = Math.max(res, dp[n][j]);
        }
        return res;
    }
}

// 方法二
class Solution {
    /**
     * @param k: An integer
     * @param prices: Given an integer array
     * @return: Maximum profit
     */
    private int update(int a, int b, int delta) {
        if (b == Integer.MIN_VALUE) {
            return a;
        }
        
        if (b + delta > a) {
            return b + delta;
        }
        
        return a;
    }  
     
    public int maxProfit(int K, int[] prices) {
        int n = prices.length;
        int i, j, k;
        if (K == 0) {
            return 0;
        }
        
        if (K >= n - 1) {
            j = 0;
            for (i = 1; i < n; ++i) {
                if (prices[i] > prices[i - 1]) {
                    j += prices[i] - prices[i - 1];
                }
            }
            
            return j;
        }
        
        int[][] f = new int[n+1][2*K+1];
        for (i = 0; i <= n; ++i) {
            for (j = 0; j <= 2*K; ++j) {
                f[i][j] = Integer.MIN_VALUE;
            }
        }
        
        f[0][0] = 0;
        for (i = 1; i <= n; ++i) {
            int delta;
            if (i == 1) {
                delta = 0;
            }
            else {
                delta = prices[i-1] - prices[i - 2];
            }
            
            f[i][0] = update(f[i][0], f[i-1][0], 0);
            for (j = 1; j <= 2 * K; j += 2) {
                if (i > 1) f[i][j] = update(f[i][j], f[i-1][j], delta);
                if (i > 1) f[i][j] = update(f[i][j], f[i-1][j-1], delta);
            }
            
            for (j = 2; j <= 2 * K; j += 2) {
                f[i][j] = update(f[i][j], f[i-1][j], 0);
                if (i > 1) f[i][j] = update(f[i][j], f[i-1][j-1], delta);
                if (i > 1) f[i][j] = update(f[i][j], f[i-1][j-2], delta);
            }
        }
        
        int res = Integer.MIN_VALUE;
        for (j = 2; j <= 2 * K; j += 2) {
            res = update(res, f[n][j], 0);
        }
        
        return res;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
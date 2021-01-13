# 买卖股票的最佳时机 IV
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/best-time-to-buy-and-sell-stock-iv/?utm_source=sc-github-wzz)
 ## 题目描述
 给定数组 `prices`, 其中第 `i` 个元素代表某只股票在第 `i` 天第价格.

**你最多可以完成 `k` 笔交易.** 问最大的利润是多少?
 ### 样例说明
 **样例 1:**

```
输入: k = 2, prices = [4, 4, 6, 1, 1, 4, 2 ,5]
输出: 6
解释: 以 4 买入, 以 6 卖出. 然后再以 1 买入, 以 5 卖出. 利润为 2 + 4 = 6.
```

**样例 2:**

```
输入: k = 1, prices = [3, 2, 1]
输出: 0
解释: 不进行交易
```
 ### 参考代码
 假设一共有 n 天, 那么这 n 天最多能够完成 n / 2 比交易, 也就是说, 当 k * 2 >= n 时, 就变成了 [买卖股票的最佳时机 II](https://www.jiuzhang.com/solution/best-time-to-buy-and-sell-stock-ii/), 反之, 我们可以作为动态规划问题解决:

定义:

- globalbest[i][j] 表示前i天，至多进行j次交易时的最大获益
- mustsell[i][j] 表示前i天，至多进行j次交易，并且第i天卖出手中的股票时的最大获益

状态转移:

- `mustsell[i][j] = max(globalbest[i - 1][j - 1], mustsell[i - 1][j]) + prices[i] - prices[i - 1]`
- `globalbest[i][j] = max(globalbest[i - 1][j], mustsell[i][j])`

边界: `mustsell[0][i] = globalbest[0][i] = 0`

优化: 滚动数组优化两个状态的空间至一维数组.
```java
// 动态规划专题班版本
class Solution {
    /**
     * @param prices: Given an integer array
     * @return: Maximum profit
     */

    public int maxProfit(int K, int[] P) {
        int n = P.length;
        if (n == 0) {
            return 0;
        }

        int i, j, k;
        if (K > n / 2) {
            // best time to buy and sell stock ii
            int tmp = 0;
            for (i = 0; i < n - 1; ++i) {
                tmp += Math.max(0, P[i + 1] - P[i]);
            }

            return tmp;
        }

        int[][] f = new int[n + 1][2 * K + 1 + 1];
        for (k = 1; k <= 2 * K + 1; ++k) {
            f[0][k] = Integer.MIN_VALUE; // impossible
        }

        f[0][1] = 0;
        for (i = 1; i <= n; ++i) {
            // 阶段1, 3, .. 2 * K + 1: f[i][j] = max{f[i-1][j], f[i-1][j-1] + Pi-1 – Pi-2}
            for (j = 1; j <= 2 * K + 1; j += 2) {
                f[i][j] = f[i - 1][j];
                if (j > 1 && i > 1 && f[i - 1][j - 1] != Integer.MIN_VALUE) {
                    f[i][j] = Math.max(f[i][j], f[i - 1][j - 1] + P[i - 1] - P[i - 2]);
                }
            }

            // 阶段2, 4.., 2K: f[i][j] = max{f[i-1][j] + Pi-1 – Pi-2, f[i-1][j-1]}
            for (j = 2; j <= 2 * K + 1; j += 2) {
                f[i][j] = f[i - 1][j - 1];
                if (i > 1 && f[i - 1][j] != Integer.MIN_VALUE) {
                    f[i][j] = Math.max(f[i][j], f[i - 1][j] + P[i - 1] - P[i - 2]);
                }
            }
        }

        int res = 0;
        for (j = 1; j <= 2 * K + 1; j += 2) {
            res = Math.max(res, f[n][j]);
        }

        return res;
    }
}

// version 2
class Solution {
    /**
     * @param k:      An integer
     * @param prices: Given an integer array
     * @return: Maximum profit
     */
    public int maxProfit(int k, int[] prices) {
        // write your code here
        if (k == 0) {
            return 0;
        }
        if (k >= prices.length / 2) {
            int profit = 0;
            for (int i = 1; i < prices.length; i++) {
                if (prices[i] > prices[i - 1]) {
                    profit += prices[i] - prices[i - 1];
                }
            }
            return profit;
        }
        int n = prices.length;
        int[][] mustsell = new int[n + 1][n + 1]; // mustSell[i][j] 表示前i天，至多进行j次交易，第i天必须sell的最大获益
        int[][] globalbest = new int[n + 1][n + 1]; // globalbest[i][j] 表示前i天，至多进行j次交易，第i天可以不sell的最大获益

        mustsell[0][0] = globalbest[0][0] = 0;
        for (int i = 1; i <= k; i++) {
            mustsell[0][i] = globalbest[0][i] = 0;
        }

        for (int i = 1; i < n; i++) {
            int gainorlose = prices[i] - prices[i - 1];
            mustsell[i][0] = 0;
            for (int j = 1; j <= k; j++) {
                mustsell[i][j] = Math.max(globalbest[(i - 1)][j - 1] + gainorlose, mustsell[(i - 1)][j] + gainorlose);
                globalbest[i][j] = Math.max(globalbest[(i - 1)][j], mustsell[i][j]);
            }
        }
        return globalbest[(n - 1)][k];
    }
};

// 方法二
class Solution {
    /**
     * @param k:      An integer
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

        int[][] f = new int[n + 1][2 * K + 1];
        for (i = 0; i <= n; ++i) {
            for (j = 0; j <= 2 * K; ++j) {
                f[i][j] = Integer.MIN_VALUE;
            }
        }

        f[0][0] = 0;
        for (i = 1; i <= n; ++i) {
            int delta;
            if (i == 1) {
                delta = 0;
            } else {
                delta = prices[i - 1] - prices[i - 2];
            }

            f[i][0] = update(f[i][0], f[i - 1][0], 0);
            for (j = 1; j <= 2 * K; j += 2) {
                if (i > 1)
                    f[i][j] = update(f[i][j], f[i - 1][j], delta);
                if (i > 1)
                    f[i][j] = update(f[i][j], f[i - 1][j - 1], delta);
            }

            for (j = 2; j <= 2 * K; j += 2) {
                f[i][j] = update(f[i][j], f[i - 1][j], 0);
                if (i > 1)
                    f[i][j] = update(f[i][j], f[i - 1][j - 1], delta);
                if (i > 1)
                    f[i][j] = update(f[i][j], f[i - 1][j - 2], delta);
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
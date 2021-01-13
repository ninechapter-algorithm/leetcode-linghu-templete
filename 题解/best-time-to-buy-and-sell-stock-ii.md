# 买卖股票的最佳时机 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/best-time-to-buy-and-sell-stock-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个数组 `prices` 表示一支股票每天的价格. 

你可以完成任意次数的交易, 不过你不能同时参与多个交易 (也就是说, 如果你已经持有这支股票, 在再次购买之前, 你必须先卖掉它).

设计一个算法求出最大的利润.
 ### 样例说明
 **样例 1:**

```
输入: [2, 1, 2, 0, 1]
输出: 2
解释: 
    1. 在第 2 天以 1 的价格买入, 然后在第 3 天以 2 的价格卖出, 利润 1
    2. 在第 4 天以 0 的价格买入, 然后在第 5 天以 1 的价格卖出, 利润 1
    总利润 2.
```

**样例 2:**

```
输入: [4, 3, 2, 1]
输出: 0
解释: 不进行任何交易, 利润为0.
```
 ### 参考代码
 贪心法: 只要相邻的两天股票的价格是上升的, 我们就进行一次交易, 获得一定利润.

这样的策略不一定是最小的交易次数, 但是一定会得到最大的利润.
```java
public class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            int diff = prices[i + 1] - prices[i];
            if (diff > 0) {
                profit += diff;
            }
        }
        return profit;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
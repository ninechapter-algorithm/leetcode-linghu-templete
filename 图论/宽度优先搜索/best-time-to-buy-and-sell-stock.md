# 买卖股票的最佳时机
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/best-time-to-buy-and-sell-stock/?utm_source=sc-github-wzz)
 ## 题目描述
 <span style="line-height: 1.42857143;">假设有一个数组，它的第i个元素是一支给定的股票在第i天的价格。</span><span style="line-height: 1.42857143;">如果你最多只允许完成一次交易(例如,一次买卖股票),设计一个算法来找出最大利润。</span>
 ### 样例说明
 **样例1**

```plain
输入: [3, 2, 3, 1, 2]
输出: 1
说明：你可以在第三天买入，第四天卖出，利润是 2 - 1 = 1
```

**样例2**

```plain
输入: [1, 2, 3, 4, 5]
输出: 4
说明：你可以在第0天买入，第四天卖出，利润是 5 - 1 = 4
```

**样例3**

```plain
输入: [5, 4, 3, 2, 1]
输出: 0
说明：你可以不进行任何操作然后也得不到任何利润
```


 ### 参考代码
 Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.
```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int min = Integer.MAX_VALUE;  //just remember the smallest price
        int profit = 0;
        for (int i : prices) {
            min = i < min ? i : min;
            profit = (i - min) > profit ? i - min : profit;
        }

        return profit;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
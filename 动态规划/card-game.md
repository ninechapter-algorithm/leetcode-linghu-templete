# 卡牌游戏
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/card-game/?utm_source=sc-github-wzz)
 ## 题目描述
 现在有一个卡牌游戏，先给出卡牌的数量`n`，再给你两个非负整数`totalProfit`、`totalCost`，然后给出每张卡牌的利润值 `a[i]`和成本值`b[i]`，现在可以从这些卡牌中任意选择若干张牌，组成一个方案，问有多少个方案满足所有选择的卡牌利润和大于`totalProfit`且成本和小于`totalCost`。
 ### 样例说明
 **样例 1:**
```
输入：n = 2，totalProfit = 3，totalCost = 5，a = [2,3]，b = [2,2] 
输出：1
解释：
此时只有一个合法的方案，就是将两个卡牌都选上，此时a[1]+a[2] = 5 > totalProfit 且 b[1] + b[2] < totalCost，满足题意。
```
**样例 2:**
```
输入：n = 3，totalProfit = 5，totalCost = 10，a = [6,7,8]，b = [2,3,5]
输出： 6
解释：
假设一个合法方案(i,j)表示选择了第i张卡牌和第j张卡牌。
则此时合法的方案有：
(1),(2),(3),(1,2),(1,3),(2,3)
```

 ### 参考代码
 使用记忆化搜索的方法
时间复杂度 $O(n * totalProfit * totalCost)$
```python
BASE = 1000000007


class Solution:
    """
    @param n: The number of cards
    @param totalProfit: The totalProfit
    @param totalCost: The totalCost
    @param a: The profit of cards
    @param b: The cost of cards
    @return: Return the number of legal plan
    """
    def numOfPlan(self, n, totalProfit, totalCost, a, b):
        return self.memo_search(0, n, totalProfit, totalCost, a, b, {})
        
    def memo_search(self, index, n, profit, cost, a, b, memo):
        if profit < 0:
            profit = -1
        if cost < 0:
            return 0
            
        if index == n:
            if 0 > profit and 0 < cost:
                return 1
            return 0

        if (index, profit, cost) in memo:
            return memo[(index, profit, cost)]
        
        select = self.memo_search(index + 1, n, profit - a[index], cost - b[index], a, b, memo)
        unselect = self.memo_search(index + 1, n, profit, cost, a, b, memo)
        
        memo[(index, profit, cost)] = (select + unselect) % BASE
        return memo[(index, profit, cost)]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
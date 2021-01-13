# 石头游戏 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/stone-game-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 有一个石头游戏。在游戏的开始的时候，玩家在 `圈` 中挑选了n堆石头。
目标是按照下面的规则将石头合并成一堆：

在游戏中的每一步，玩家可以合并两堆相邻的石头为新的一堆石头。分数就是新的石头堆的石头个数。你需要找到最小的总分。
 ### 样例说明
 例1：
```
输入：
[1,1,4,4]
输出：18
解释：
合并第二个和第三个=> [2,4,4]，得分+2
2.合并前两个=> [6,4]，得分+6
3.合并最后两个=> [10]，得分+10
```

例2：
```
输入：
[1,1,1,1]
输出：8
解释：
合并第一个和第二个=> [2,1,1]，得分+2
2.合并后两个=> [2,2]，得分+2
3.合并最后两个=> [4]，得分+4
```
 ### 参考代码
 动态规划。
dp[i][j]代表从i合并到j的最少花费。
转移方程为dp[i][j] = min（dp[i][k] + dp[k+1][j] + sum[j + 1] - sum[i]）
```python
class Solution:
    # @param {int[]} A an integer array
    # @return {int} an integer
    def stoneGame2(self, A):
        # Write your code here
        n = len(A)
        if n <= 1:
            return 0

        s = [0]
        dp = [[sys.maxint for i in xrange(2 * n)] for j in xrange(2 * n)]
        for i in xrange(2 * n):
            s.append(s[-1] + A[i % n])
            dp[i][i] = 0

        for l in xrange(2, 2 * n + 1):
            for i in xrange(2 * n):
                j = i + l - 1
                if j >= 2 * n:
                    continue
                for k in xrange(i, j):
                    dp[i][j] = min(dp[i][k] + dp[k+1][j] + s[j + 1] - s[i], dp[i][j])

        ans = sys.maxint
        for i in xrange(n):
            ans = min(ans, dp[i][i + n - 1])
        return ans
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
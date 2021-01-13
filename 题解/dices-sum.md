# 骰子求和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/dices-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 扔 *n* 个骰子，向上面的数字之和为 *S*。给定 *n*，请列出所有可能的 *S* 值及其相应的概率。
 ### 样例说明
 **样例 1：**

```
输入：n = 1
输出：[[1, 0.17], [2, 0.17], [3, 0.17], [4, 0.17], [5, 0.17], [6, 0.17]]
解释：掷一次骰子，向上的数字和可能为1,2,3,4,5,6，出现的概率均为 0.17。
```

**样例 2：**

```
输入：n = 2
输出：[[2,0.03],[3,0.06],[4,0.08],[5,0.11],[6,0.14],[7,0.17],[8,0.14],[9,0.11],[10,0.08],[11,0.06],[12,0.03]]
解释：掷两次骰子，向上的数字和可能在[2,12]，出现的概率是不同的。
```

 ### 参考代码
 ```python
class Solution:
    # @param {int} n an integer
    # @return {tuple[]} a list of tuple(sum, probability)
    def dicesSum(self, n):
        # Write your code here
        results = []
        f = [[0 for j in xrange(6 * n + 1)] for i in xrange(n + 1)]
        
        for i in xrange(1, 7):
            f[1][i] = 1.0 / 6.0
        for i in xrange(2, n + 1):
            for j in xrange(i, 6 * n + 1):
                for k in xrange(1, 7):
                    if j > k:
                        f[i][j] += f[i - 1][j - k]
                f[i][j] /= 6.0

        for i in xrange(n, 6 * n + 1):
            results.append((i, f[n][i]))

        return results

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
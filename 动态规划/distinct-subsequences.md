# 不同的子序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/distinct-subsequences/?utm_source=sc-github-wzz)
 ## 题目描述
 给定字符串 `S` 和 `T`, 计算 `S` 的所有子序列中有多少个 `T`.

子序列字符串是原始字符串删除一些(或零个)字符之后得到的字符串, 并且要求剩下的字符的相对位置不能改变. (比如 `"ACE"` 是 `ABCDE` 的一个子序列, 而 `"AEC"` 不是)
 ### 样例说明
 **样例 1:**

```
输入: S = "rabbbit", T = "rabbit"
输出: 3
解释: 你可以删除 S 中的任意一个 'b', 所以一共有 3 种方式得到 T.
```

**样例 2:**

```
输入: S = "abcd", T = ""
输出: 1
解释: 只有删除 S 中的所有字符这一种方式得到 T
```
 ### 参考代码
 多达5种解法与详细解释请参见九章微博：<http://weibo.com/3948019741/BDqR6hMdY>
```python
class Solution: 
    # @param S, T: Two string.
    # @return: Count the number of distinct subsequences
    def numDistinct(self, S, T):
        # write your code here
        dp = [[0 for j in range(len(T) + 1)] for i in range(len(S) + 1)]
        for i in range(len(S) + 1):
   			dp[i][0] = 1
        for i in xrange(len(S)):
            for j in xrange(len(T)):
                if S[i] == T[j]:
                    dp[i+1][j+1] = dp[i][j+1] + dp[i][j]
                else:
                    dp[i+1][j+1] = dp[i][j + 1]
        return dp[len(S)][len(T)]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
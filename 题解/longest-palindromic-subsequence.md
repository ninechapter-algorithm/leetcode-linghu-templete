# 最长的回文序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-palindromic-subsequence/?utm_source=sc-github-wzz)
 ## 题目描述
 给一字符串 s, 找出在 s 中的最长回文子序列的长度. 你可以假设 s 的最大长度为 `1000`.
 ### 样例说明
 **样例1**
```
输入： "bbbab"
输出： 4
解释：
一个可能的最长回文序列为 "bbbb"
```
**样例2**
```
输入： "bbbbb"
输出： 5
```
 ### 参考代码
 对于任意字符串，如果头尾字符相同，那么字符串的最长子序列等于去掉首尾的字符串的最长子序列加上首尾；如果首尾字符不同，则最长子序列等于去掉头的字符串的最长子序列和去掉尾的字符串的最长子序列的较大者。

设`dp[i][j]`表示第i到第j个字符间的最长回文序列的长度（i<=j）

状态转移方程：

$dp[i][j]=dp[i+1][j-1] + 2\qquad if(str[i]==str[j])$

$dp[i][j]=max(dp[i+1][j],dp[i][j-1])\quad  if(str[i]!=str[j])$
```python
class Solution:
    """
    @param s: the maximum length of s is 1000
    @return: the longest palindromic subsequence's length
    """
    def longestPalindromeSubseq(self, s):
        length = len(s)
        if length == 0:
            return 0
        dp = [[0] * length for _ in range(length)]
        for i in range(length - 1, -1, -1):
            dp[i][i] = 1
            for j in range(i + 1, length):
                if s[i] == s[j]:
                    dp[i][j] = dp[i + 1][j - 1] + 2
                else:
                    dp[i][j] = max(dp[i + 1][j], dp[i][j - 1])
        return dp[0][length - 1]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 解码方法
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/decode-ways/?utm_source=sc-github-wzz)
 ## 题目描述
 有一个消息包含`A-Z`通过以下规则编码
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
现在给你一个加密过后的消息，问有几种解码的方式
 ### 样例说明
 **样例 1:**

```
输入: "12"
输出: 2
解释: 它可以被解码为 AB (1 2) 或 L (12).
```

**样例 2:**

```
输入: "10"
输出: 1
```
 ### 参考代码
 动态规划.

设定状态: f[i] 表示字符串前i位有多少种解码方案

状态转移方程:

```
初始化 f 数组为 0
若字符串中 s[i] 表示的阿拉伯数字在 1~9 范围内, f[i] += f[i-1]
若s[i-1]和s[i]连起来表示的数字在 10~26 范围内, f[i] += f[i-2] (若i==1, 则f[i] += 1)
```

边界: f[0] = 1

特判: 

1. 如果字符串以 `'0'` 开头, 则直接返回0.
2. 如果运算中发现 f[i] == 0, 则说明此处无法解码, 同样直接返回0.
```python
class Solution:
    # @param {string} s a string,  encoded message
    # @return {int} an integer, the number of ways decoding
    def numDecodings(self, s):
        if s == "" or s[0] == '0':
            return 0

        dp = [1, 1]
        for i in range(2,len(s) + 1):
            if 10 <= int(s[i - 2 : i]) <=26 and s[i - 1] != '0':
                dp.append(dp[i - 1] + dp[i - 2])
            elif int(s[i-2 : i]) == 10 or int(s[i - 2 : i]) == 20:
                dp.append(dp[i - 2])
            elif s[i-1] != '0':
                dp.append(dp[i-1])
            else:
                return 0

        return dp[len(s)]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
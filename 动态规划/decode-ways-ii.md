# 解码方式 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/decode-ways-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 使用以下映射方式将 A-Z 的消息编码为数字:
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
除此之外, 编码的字符串也可以包含字符 `*`, 它代表了 1 到 9 的数字中的其中一个.给出包含数字和字符 `*` 的编码消息, 返回所有解码方式的数量. 因为结果可能很大, 所以结果需要对 10^9 + 7 取模
 ### 样例说明
 **样例1**

```plain
输入: "*"
输出: 9
说明: 你可以译码为 "A", "B", "C", "D", "E", "F", "G", "H", "I".
```

**样例2**

```plain
输入: "1*"
输出: 18
```


 ### 参考代码
 ```python
class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if s == None:
            return 0
        mod = 1000000007
        n = len(s)
        f = [0] * (n + 1)
        f[0] = 1
        for i in xrange(1, n + 1):
            if s[i - 1] == '*':
                f[i] = (f[i] + 9 * f[i - 1]) % mod
                if i >= 2:
                    t = 0
                    if s[i - 2] == '*':
                        f[i] = (f[i] + 15 * f[i - 2]) % mod
                    elif s[i - 2] == '1':
                        f[i] = (f[i] + 9 * f[i - 2]) % mod
                    elif s[i - 2] == '2':
                        f[i] = (f[i] + 6 * f[i - 2]) % mod
            else:
                if s[i - 1] >= '1' and s[i - 1] <= '9':
                    f[i] = (f[i] + f[i - 1]) % mod
                if i >= 2:
                    if s[i - 2] == '*':
                        t = 0
                        if s[i - 1] >= '0' and s[i - 1] <= '6':
                            f[i] = (f[i] + 2 * f[i - 2]) % mod
                        elif s[i - 1] >= '7' and s[i - 1] <= '9':
                            f[i] = (f[i] + f[i - 2]) % mod
                    else:
                        twoDigits = int(s[i - 2 : i])
                        if twoDigits >= 10 and twoDigits <= 26:
                            f[i] = (f[i] + f[i - 2]) % mod
        return f[n]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
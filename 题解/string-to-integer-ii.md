# String to Integer II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/string-to-integer-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 1769
 ### 样例说明
 1769
 ### 参考代码
 ```python
class Solution:
    # @param str: a string
    # @return an integer
    def atoi(self, str):
        if len(str) == 0:
            return 0
        sgn, num, p = 0, 0, 0
        imin, imax = -1<<31, (1<<31)-1
        while str[p] == ' ':
            p  = p + 1
        if str[p] == '-' or str[p] == '+':
            sgn = 1 if str[p] == '-' else 0
            p = p + 1
        while p < len(str) and str[p] >= '0' and str[p] <= '9':
            num = num * 10 + ord(str[p]) - ord('0')
            x = -num if sgn else num
            if x < imin: return imin
            if x > imax: return imax
            p = p + 1
        return -num if sgn else num

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
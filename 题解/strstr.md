# strstr
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/strstr/?utm_source=sc-github-wzz)
 ## 题目描述
 1770
 ### 样例说明
 1770
 ### 参考代码
 ```python
class Solution:
    """
    @param: source: source string to be scanned.
    @param: target: target string containing the sequence of characters to match
    @return: a index to the first occurrence of target in source, or -1  if target is not part of source.
    """
    def strStr(self, source, target):
        # write your code here
        if source is None or target is None:
            return -1

        if len(source) < len(target):
            return -1
        if len(target) == 0:
            return 0
        for i in range(len(source)-len(target) + 1):
            j = 0
            while j < len(target):
                if source[i + j] == target[j]:
                    j = j + 1
                else:
                    j = 0
                    break
            if j == len(target):
                return i
        return -1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
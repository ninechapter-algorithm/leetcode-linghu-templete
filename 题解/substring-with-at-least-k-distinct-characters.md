# 至少K个不同字符的子串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/substring-with-at-least-k-distinct-characters/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个仅包含小写字母的字符串 `S`.

返回 `S` 中至少包含 `k` 个不同字符的子串的数量.
 ### 样例说明
 **样例 1:**

```
输入: S = "abcabcabca", k = 4
输出: 0
解释: 字符串中一共就只有 3 个不同的字符.
```

**样例 2:**

```
输入: S = "abcabcabcabc", k = 3
输出: 55
解释: 任意长度不小于 3 的子串都含有 a, b, c 这三个字符.
    比如,长度为 3 的子串共有 10 个, "abc", "bca", "cab" ... "abc"
    长度为 4 的子串共有 9 个, "abca", "bcab", "cabc" ... "cabc"
    ...
    长度为 12 的子串有 1 个, 就是 S 本身.
    所以答案是 1 + 2 + ... + 10 = 55.
```
 ### 参考代码
 ```python
class Solution:
    """
    @param s: a string
    @param k: an integer
    @return: the number of substrings there are that contain at least k distinct characters
    """
    def kDistinctCharacters(self, s, k):
        left = 0
        counter = {}
        answer = 0
        for right in range(len(s)):
            counter[s[right]] = counter.get(s[right], 0) + 1
            while left <= right and len(counter) >= k:
                counter[s[left]] -= 1
                if counter[s[left]] == 0:
                    del counter[s[left]]
                left += 1
                    
            if len(counter) == k - 1 and left > 0 and s[left - 1] not in counter:
                answer += left
                
        
        return answer
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
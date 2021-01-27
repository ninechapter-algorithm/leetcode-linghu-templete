# 最多有k个不同字符的最长子字符串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-substring-with-at-most-k-distinct-characters/?utm_source=sc-github-wzz)
 ## 题目描述
 给定字符串*S*，找到最多有k个不同字符的最长子串*T*。
 ### 样例说明
 **样例 1:**

```
输入: S = "eceba" 并且 k = 3
输出: 4
解释: T = "eceb"
```

**样例 2:**

```
输入: S = "WORLD" 并且 k = 4
输出: 4
解释: T = "WORL" 或 "ORLD"
 ### 参考代码
 一次遍历即可
遍历的同时记录: 每个字符出现的次数, 当前子串中不同字符的个数
其中定义一个变量记录左边界, 当前子串即左边界到遍历位置对应的子串
如果不同字符的个数超过k, 则向右调整左边界即可, 遍历同时维护最长子串长度即可
```python
class Solution:
    """
    @param s: A string
    @param k: An integer
    @return: An integer
    """
    def lengthOfLongestSubstringKDistinct(self, s, k):
        if not s:
            return 0
            
        counter = {}
        left = 0
        longest = 0
        for right in range(len(s)):
            counter[s[right]] = counter.get(s[right], 0) + 1
            while left <= right and len(counter) > k:
                counter[s[left]] -= 1
                if counter[s[left]] == 0:
                    del counter[s[left]]
                left += 1
            
            longest = max(longest, right - left + 1)
        return longest
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
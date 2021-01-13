# 单词拆分 I
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-break/?utm_source=sc-github-wzz)
 ## 题目描述
 给定字符串 s 和单词字典 dict，确定 s 是否可以分成一个或多个以空格分隔的子串，并且这些子串都在字典中存在。
 ### 样例说明
 ```
样例 1:
	输入:  "lintcode", ["lint", "code"]
	输出:  true

样例 2:
	输入: "a", ["a"]
	输出:  true
	
```


 ### 参考代码
 使用《九章算法班》中讲过的划分型动态规划算法
- state: `dp[i]` 表示前 i 个字符是否能够被划分为若干个单词
- function: `dp[i]` = or{`dp[j]` and j + 1~i 是一个单词}
```
[[python]]
class Solution:
    """
    @param: s: A string
    @param: dict: A dictionary of words dict
    @return: A boolean
    """
    def wordBreak(self, s, wordSet):
        if not s:
            return True
            
        n = len(s)
        dp = [False] * (n + 1)
        dp[0] = True
        
        max_length = max([
            len(word)
            for word in wordSet
        ]) if wordSet else 0
        
        for i in range(1, n + 1):
            for l in range(1, max_length + 1):
                if i < l:
                    break
                if not dp[i - l]:
                    continue
                word = s[i - l:i]
                if word in wordSet:
                    dp[i] = True
                    break
        
        return dp[n]
[[java]]
public class Solution {
    /*
     * @param s: A string
     * @param dict: A dictionary of words dict
     * @return: A boolean
     */
    public boolean wordBreak(String s, Set<String> dict) {
        if (s == null) {
            return true;
        }
        
        int maxLength = 0;
        for (String word : dict) {
            maxLength = Math.max(maxLength, word.length());
        }
      
        int n = s.length();
        boolean[] dp = new boolean[n + 1];
        dp[0] = true;
        
        for (int i = 1; i <= n; i++) {
            for (int l = 1; l <= maxLength; l++) {
                if (i < l) {
                    break;
                }
                if (!dp[i - l]) {
                    continue;
                }
                String word = s.substring(i - l, i);
                if (dict.contains(word)) {
                    dp[i] = true;
                    break;
                }
            }
        }
        
        return dp[n];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
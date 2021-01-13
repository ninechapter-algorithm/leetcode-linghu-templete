# 不同的子序列 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/distinct-subsequences-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串 `S`，计算 `S` 的不同非空子序列的个数。

因为结果可能很大，所以返回答案模 `10^9 + 7`.
 ### 样例说明
 **示例 1:**
```
输入: "abc"
输出: 7
解释: 7 个不同的子序列分别是 "a", "b", "c", "ab", "ac", "bc", 以及 "abc"。
```
**示例 2:**
```
输入: "aba"
输出: 6
解释: 6 个不同的子序列分别是 "a", "b", "ab", "ba", "aa" 以及 "aba"。
```
**示例 3:**
```
输入: "aaa"
输出: 3
解释: 3 个不同的子序列分别是 "a", "aa" 以及 "aaa"。
```
 ### 参考代码
 ```
[[python]]
MOD = 10 ** 9 + 7


class Solution:
    """
    @param S: The string s
    @return: The number of distinct, non-empty subsequences of S.
    """
    def distinctSubseqII(self, S):
        n = len(S)
        
        # state: dp[i] 表示以下标 i 作为 subseq 的最后一个字符
        # 的方案总数
        dp = [0] * n
        
        # initialization: 如果 i 是第一个出现 S[i] 这个字符的位置，那么 dp[i] = 1
        visited = set()
        for i in range(n):
            if S[i] not in visited:
                dp[i] = 1
            visited.add(S[i])
        
        # function: dp[i] = sigma{dp[j]}, j 到 i - 1 之间没有 S[i]
        for i in range(n):
            for j in range(i - 1, -1, -1):
                dp[i] = (dp[i] + dp[j]) % MOD
                if S[i] == S[j]:
                    break
        
        # answer: 以所有位置结尾的方案总数之和
        return sum(dp) %  MOD
[[java]]
public class Solution {
    /**
     * @param S: The string s
     * @return: The number of distinct, non-empty subsequences of S.
     */
    private int MOD = 1000000007; 
     
    public int distinctSubseqII(String S) {
        int n = S.length();
        
        // state: dp[i] 表示以下标 i 作为 subseq 的最后一个字符
        // 的方案总数
        int[] dp = new int[n];
        
        // initialization: 如果 i 是第一个出现 S.charAt(i) 这个字符的位置，那么 dp[i] = 1
        Set<Character> visited = new HashSet<>();
        for (int i = 0; i < n; i++) {
            if (!visited.contains(S.charAt(i))) {
                dp[i] = 1;
            }
            visited.add(S.charAt(i));
        }
        
        // function: dp[i] = sigma{dp[j]}, j 到 i - 1 之间没有 S[i]
        for (int i = 0; i < n; i++) {
            for (int j = i - 1; j >= 0; j--) {
                dp[i] = (dp[i] + dp[j]) % MOD;
                if (S.charAt(i) == S.charAt(j)) {
                    break;
                }
            }
        }
        
        // answer: 以所有位置结尾的方案总数之和
        int answer = 0;
        for (int i = 0; i < dp.length; i++) {
            answer = (answer + dp[i]) % MOD;
        }
        return answer;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 最长重复子序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-repeating-subsequence/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个字符串，找到最长的重复子序列的长度，并且这两个子序列不能在相同位置有同一元素。
比如：在两个子序列中的第i个元素不能在原来的字符串中有相同的下标。
 ### 样例说明
 例1:
```
输入:"aab"
输出:1
解释:
两个子序列是a（第一个）和a（第二个）。
请注意，b不能被视为子序列的一部分，因为它在两者中都是相同的索引。
```


例2:
```
输入:"abc"
输出:0
解释:
没有重复的序列
```


例3:
```
输入:"aabb"
输出:2
解释:
有两个相同的子序列"ab". 其中第一个子序列是s[0] + s[2], 第二个子序列是s[1]+s[3], 所以重复子序列的长度为2.
```

 ### 参考代码
 动态规划。
dp[i][j] 代表前i个与前j个匹配的最大长度。
若字符相同而位置不同，即可转移。
```java
public class Solution {
    /**
     * @param str a string
     * @return the length of the longest repeating subsequence
     */
    public int longestRepeatingSubsequence(String str) {
        // Write your code here
        int n = str.length();

        int[][] dp = new int[n + 1][n + 1];

        for (int i = 0; i <= n; ++i)
            for (int j = 0; j <= n; ++j)
                dp[i][j] = 0;
     
        for (int i = 1; i <= n; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (str.charAt(i - 1) == str.charAt(j - 1) && i != j)
                    dp[i][j] = dp[i - 1][j - 1] + 1;                               
                else
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j]);
            }
        }
        return dp[n][n];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
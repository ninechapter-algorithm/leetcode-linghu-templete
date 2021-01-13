# 最长公共子串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-common-substring/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出两个字符串，找到最长公共子串，并返回其长度。</p><p><br></p>
 ### 样例说明
 
```
样例 1:
	输入:  "ABCD" and "CBCE"
	输出:  2
	
	解释:
	最长公共子串是 "BC"


样例 2:
	输入: "ABCD" and "EACB"
	输出:  1
	
	解释: 
	最长公共子串是 'A' 或 'C' 或 'B'
```
 ### 参考代码
 http://www.lintcode.com/en/problem/longest-common-substring/

Given two strings, find the longest common substring.

Return the length of it.

Note
The characters in substring should occur continiously in original string. This is different with subsequnce.


Dp[i][j] 表示A的前i个字符与B的前j个字符中，且以第i个和第j个为结尾的公共子串的长度。
暴力枚举所有的结尾。
```java
// 严格的说，这个算法是递推，而不是动态规划，但是可以用动态规划的四要素去分析换个解答。
// 为什么不是动态规划？因为最暴力的方式也就是 O(n^3) 可以找到A所有的Substring然后看看在不在B里。
public class Solution {
    /**
     * @param A, B: Two string.
     * @return: the length of the longest common substring.
     */
    public int longestCommonSubstring(String A, String B) {
        // state: f[i][j] is the length of the longest lcs
        // ended with A[i - 1] & B[j - 1] in A[0..i-1] & B[0..j-1]
        int n = A.length();
        int m = B.length();
        int[][] f = new int[n + 1][m + 1];
        
        // initialize: f[i][j] is 0 by default
        
        // function: f[i][j] = f[i - 1][j - 1] + 1 or 0
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    f[i][j] = f[i - 1][j - 1] + 1;
                } else {
                    f[i][j] = 0;
                }
            }
        }
        
        // answer: max{f[i][j]}
        int max = 0;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                max = Math.max(max, f[i][j]);
            }
        }
        
        return max;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
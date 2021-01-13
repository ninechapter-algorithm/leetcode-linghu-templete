# 一和零
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/ones-and-zeroes/?utm_source=sc-github-wzz)
 ## 题目描述
 在计算机世界中, 由于资源限制, 我们一直想要追求的是产生最大的利益.
现在，假设你分别是 m个 `0s` 和 n个 `1s` 的统治者. 另一方面, 有一个只包含 `0s` 和 `1s` 的字符串构成的数组.
现在你的任务是找到可以由 m个 `0s` 和 n个 `1s` 构成的字符串的最大个数. 每一个 `0` 和 `1` 均只能使用一次
 ### 样例说明
 **样例1**
```
输入：
["10", "0001", "111001", "1", "0"]
5
3
输出： 4
解释：这里总共有 4 个字符串可以用 5个 0s 和 3个 1s来构成, 它们是 "10", "0001", "1", "0"。
```
**样例2**
```
输入：
["10", "0001", "111001", "1", "0"]
7
7
输出： 5
解释： 所有字符串都可以由7个 0s 和 7个 1s来构成.
```
 ### 参考代码
 设dp[i][j][k]表示前i个字符串，使用j个0s，k个1s最多能选择的个数。
$dp[i][j][k]=max(dp[i-1][j][k],dp[i-1][j-cnt_{zero}(str[i])][k-cnt_{one}(str[i])])$
```java
//方法一 未进行空间复杂度优化：
public class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        int[][][] dp = new int[strs.length + 1][m + 1][n + 1];
        for (int i = 1; i <= strs.length; i++) {
            int[] cost = count(strs[i - 1]);
            for (int j = 0; j <= m; j++) {
                for (int k = 0; k <= n; k++) {
                    if (j >= cost[0] && k >= cost[1]) {
                        dp[i][j][k] = Math.max(dp[i - 1][j][k], dp[i - 1][j - cost[0]][k - cost[1]] + 1);
                    } else {
                        dp[i][j][k] = dp[i - 1][j][k];
                    }
                }
            }
        }
        return dp[strs.length][m][n];
    }

    public int[] count(String str) {
        int[] cost = new int[2];
        for (int i = 0; i < str.length(); i++)
            cost[str.charAt(i) - '0']++;
        return cost;
    }
};
// 方法二 进行空间复杂度优化：
public class Solution {
    /**
     * @param strs an array with strings include only 0 and 1
     * @param m an integer
     * @param n an integer
     * @return find the maximum number of strings
     */
    public int findMaxForm(String[] A, int m, int n) {
        if (A.length == 0) {
            return 0;
        }
        
        int T = A.length;
        int[] cnt0 = new int[T];
        int[] cnt1 = new int[T];
        int i, j, k;
        for (i = 0; i < T; ++i) {
            char[] s = A[i].toCharArray();
            cnt0[i] = cnt1[i] = 0;
            for (j = 0; j < s.length; ++j) {
                if (s[j] == '0') {
                    ++cnt0[i];
                }
                else {
                    ++cnt1[i];
                }
            }
        }
        
        int[][] f = new int[m + 1][n + 1];
        for (i = 0; i <= T; ++i) {
            for (j = m; j >= 0; --j) {
                for (k = n; k >= 0; --k) {
                    if (i == 0) {
                        f[j][k] = 0;
                        continue;
                    }
                    
                    if (j >= cnt0[i - 1] && k >= cnt1[i - 1]) {
                        // new              // old    // old
                        f[j][k] = Math.max(f[j][k], f[j - cnt0[i - 1]][k - cnt1[i - 1]] + 1);
                    }
                }
            }
        }
        
        return f[m][n];
    }
}

// 动态规划专题班版本
public class Solution {
    /**
     * @param strs: an array with strings include only 0 and 1
     * @param m: An integer
     * @param n: An integer
     * @return: find the maximum number of strings
     */
    public int findMaxForm(String[] A, int m, int n) {
        if (A.length == 0) {
            return 0;
        }
        
        int T = A.length;
        int[] cnt0 = new int[T];
        int[] cnt1 = new int[T];
        int i, j, k;
        for (i = 0; i < T; ++i) {
            cnt0[i] = cnt1[i] = 0;
            char[] s = A[i].toCharArray();
            for (j = 0; j < s.length; ++j) {
                if (s[j] == '0') {
                    ++cnt0[i];
                }
                else {
                    ++cnt1[i];
                }
            }
        }
        
        int[][][] f = new int[T + 1][m + 1][n + 1];
        for (i = 0; i <= m; ++i) {
            for (j = 0; j <= n; ++j) {
                f[0][i][j] = 0;
            }
        }
        
        int res = 0;
        for (i = 1; i <= T; ++i) {
            for (j = 0; j <= m; ++j) {
                for (k = 0; k <= n; ++k) {
                    // do not take A[i - 1]
                    f[i][j][k] = f[i - 1][j][k];
                    
                    // take A[i - 1]
                    if (j >= cnt0[i - 1] && k >= cnt1[i - 1]) {
                        f[i][j][k] = Math.max(f[i][j][k], f[i - 1][j - cnt0[i - 1]][k - cnt1[i - 1]] + 1);
                    }
                    
                    if (i == T) {
                        res = Math.max(res, f[i][j][k]);
                    }
                }
            }
        }
        
        return res;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
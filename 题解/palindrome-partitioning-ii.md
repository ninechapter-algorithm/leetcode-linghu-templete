# 分割回文串 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/palindrome-partitioning-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定字符串 `s`, 需要将它分割成一些子串, 使得每个子串都是回文串.

最少需要分割几次?
 ### 样例说明
 **样例 1:**

```
输入: "a"
输出: 0
解释: "a" 本身就是回文串, 无需分割
```

**样例 2:**

```
输入: "aab"
输出: 1
解释: 将 "aab" 分割一次, 得到 "aa" 和 "b", 它们都是回文串.
```
 ### 参考代码
 与 [136. 分割回文串](https://www.lintcode.com/problem/palindrome-partitioning/description?_from=ladder&&fromId=80) 不同, 这道题目不需要求所有方案, 而是求最小次数 -- 最优解问题.

可以看作序列型动态规划问题, 设定 dp[i] 表示原串的前 i 个字符最少分割多少次可以使得到的都是回文子串.

如果 s 前 i 个字符组成的子串本身就是回文串, 则 dp[i] = 0, 否则:

```C++
dp[i] = min{dp[j] + 1} (j < i 并且 s[j + 1], s[j + 2], ... , s[i] 是回文串)
```

如果想要是 O($n^2$) 的时间复杂度 (n 是 s 的长度), 需要事先求出来回文串信息, 在状态转移时可以 O(1) 地知道一段子串是否回文的.
```cpp
class Solution {
public:
    /**
     * @param s a string
     * @return an integer
     */
    int minCut(string s) {
        int n = s.length();
        int f[n + 1];
        vector<vector<bool>> isPalin(n, vector<bool>(n, false));

        for (int i = 0; i < n; i++) {
            isPalin[i][i] = true;
            if (i + 1 < n) {
                isPalin[i][i + 1] = (s[i] == s[i + 1]);
            }
        }

        for (int i = n - 1; i >= 0; i--) {
            for (int j = i + 2; j < n; j++) {
                isPalin[i][j] = isPalin[i + 1][j - 1] && (s[i] == s[j]);
            }
        }

        f[0] = -1;
        for (int i = 1; i <= n; i++) {
            f[i] = i - 1;
            for (int j = 0; j < i; j++) {
                if (isPalin[j][i - 1]) {
                    f[i] = min(f[i], f[j] + 1);
                }
            }
        }

        return f[n];
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
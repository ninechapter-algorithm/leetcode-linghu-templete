# 最长公共子序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-common-subsequence/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出两个字符串，找到最长公共子序列(LCS)，返回LCS的长度。</p>
 ### 样例说明
 ```
样例 1:
	输入:  "ABCD" and "EDCA"
	输出:  1
	
	解释:
	LCS 是 'A' 或  'D' 或 'C'


样例 2:
	输入: "ABCD" and "EACB"
	输出:  2
	
	解释: 
	LCS 是 "AC"
```

 ### 参考代码
 使用九章算法强化班和动态规划专题班中讲的匹配型动态规划
```python
class Solution:
    """
    @param A: A string
    @param B: A string
    @return: The length of longest common subsequence of A and B
    """
    def longestCommonSubsequence(self, A, B):
        n, m = len(A), len(B)
        f = [[0] * (m + 1) for i in range(n + 1)]
        for i in range(1, n + 1):
            for j in range(1, m + 1):
                f[i][j] = max(f[i][j - 1], f[i - 1][j])
                if A[i - 1] == B[j - 1]:
                    f[i][j] = max(f[i][j], f[i - 1][j - 1] + 1)
        return f[n][m]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
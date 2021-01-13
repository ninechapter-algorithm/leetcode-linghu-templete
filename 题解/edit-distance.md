# 编辑距离
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/edit-distance/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出两个单词word1和word2，计算出将word1 转换为word2的最少操作次数。</p><p>你总共三种操作方法：</p><p></p><ul><li><span style="line-height: 1.42857143;">插入一个字符</span></li><li><span style="line-height: 1.42857143;">删除一个字符</span></li><li><span style="line-height: 1.42857143;">替换一个字符</span><br></li></ul><p></p>
 ### 样例说明
 **样例 1:**

```
输入: 
"horse"
"ros"
输出: 3
解释: 
horse -> rorse (替换 'h' 为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```

**样例 2:**

```
输入: 
"intention"
"execution"
输出: 5
解释: 
intention -> inention (删除 't')
inention -> enention (替换 'i' 为 'e')
enention -> exention (替换 'n' 为 'x')
exention -> exection (替换 'n' 为 'c')
exection -> execution (插入 'u')
```
 ### 参考代码
 使用九章算法强化班，动态规划专题班中讲过的匹配型动态规划
f[i][j] 代表第一个字符串以i结尾匹配上（编辑成）第二个字符串以j结尾的字符串，最少需要多少次编辑。
通过去判断i与j的匹配关系来变为更小的状态。
```
[[python]]
class Solution:
    """
    @param word1: A string
    @param word2: A string
    @return: The minimum number of steps.
    """
    def minDistance(self, word1, word2):
        n, m = len(word1), len(word2)
        f = [[0] * (m + 1) for _ in range(n + 1)]
        
        for i in range(n + 1):
            f[i][0] = i
        for j in range(m + 1):
            f[0][j] = j

        for i in range(1, n + 1):
            for j in range(1, m + 1):
                if word1[i - 1] == word2[j - 1]:
                    f[i][j] = min(f[i - 1][j - 1], f[i - 1][j] + 1, f[i][j - 1] + 1)
                    # equivalent to f[i][j] = f[i - 1][j - 1]
                else:
                    f[i][j] = min(f[i - 1][j - 1], f[i - 1][j], f[i][j - 1]) + 1
                        
        return f[n][m]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
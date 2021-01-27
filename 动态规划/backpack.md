# 背包问题
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/backpack/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>在n个物品中挑选若干物品装入背包，最多能装多满？假设背包的大小为m，每个物品的大小为A[i]</p>
 ### 样例说明
 ```
样例 1:
	输入:  [3,4,8,5], backpack size=10
	输出:  9

样例 2:
	输入:  [2,3,5,7], backpack size=12
	输出:  12
	
```
 ### 参考代码
 传统的背包问题解法。二维动态规划。
```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @return: The maximum size
    """
    def backPack(self, m, A):
        n = len(A)
        f = [[False] * (m + 1) for _ in range(n + 1)]
        
        f[0][0] = True
        for i in range(1, n + 1):
            f[i][0] = True
            for j in range(1, m + 1):
                if j >= A[i - 1]:
                    f[i][j] = f[i - 1][j] or f[i - 1][j - A[i - 1]]
                else:
                    f[i][j] = f[i - 1][j]
                    
        for i in range(m, -1, -1):
            if f[n][i]:
                return i
        return 0
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
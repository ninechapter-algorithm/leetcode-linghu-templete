# 石子归并
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/stone-game/?utm_source=sc-github-wzz)
 ## 题目描述
 有一个石子归并的游戏。最开始的时候，有n堆石子排成一列，目标是要将所有的石子合并成一堆。合并规则如下：

1. 每一次可以合并相邻位置的两堆石子
2. 每次合并的代价为所合并的两堆石子的重量之和

求出最小的合并代价。
 ### 样例说明
 **样例 1:**

```
输入: [3, 4, 3]
输出: 17
```

**样例 2:**

```
输入: [4, 1, 1, 4]
输出: 18
解释: 
  1. 合并第二堆和第三堆 => [4, 2, 4], score = 2
  2. 合并前两堆 => [6, 4]，score = 8
  3. 合并剩余的两堆 => [10], score = 18
```
 ### 参考代码
 使用四边形不等式优化之后的算法，时间复杂度 $O(n^2)$
记录 cut[i][j] 代表使得 dp[i][j] 获得最优值的那个划分方案（切割位置）
可以证明（证明太长就不写了） `cut[i][j - 1] <= cut[i][j] <= cut[i + 1][j]`
```python
class Solution:
    """
    @param A: An integer array
    @return: An integer
    """
    def stoneGame(self, A):
        n = len(A)
        if n < 2:
            return 0
            
        # dp[i][j] => minimum cost merge from i to j
        dp = [[0] * n for _ in range(n)]
        # cut[i][j] => the best middle point that make dp[i][j] has the minimum cost
        cut = [[0] * n for _ in range(n)]
        # range_sum[i][j] => A[i] + A[i + 1] ... + A[j]
        range_sum = self.get_range_sum(A)
        
        for i in range(n - 1):
            dp[i][i + 1] = A[i] + A[i + 1]
            cut[i][i + 1] = i
            
        # enumerate the range size first, start point second
        for length in range(3, n + 1):
            for i in range(n - length + 1):
                j = i + length - 1
                dp[i][j] = sys.maxsize
                for mid in range(cut[i][j - 1], cut[i + 1][j] + 1):
                    if dp[i][j] > dp[i][mid] + dp[mid + 1][j] + range_sum[i][j]:
                        dp[i][j] = dp[i][mid] + dp[mid + 1][j] + range_sum[i][j]
                        cut[i][j] = mid
        
        return dp[0][n - 1]
                    
    def get_range_sum(self, A):
        n = len(A)
        range_sum = [[0] * n for _ in range(len(A))]
        for i in range(n):
            range_sum[i][i] = A[i]
            for j in range(i + 1, n):
                range_sum[i][j] = range_sum[i][j - 1] + A[j]
        return range_sum
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 旅行商问题
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/traveling-salesman-problem/?utm_source=sc-github-wzz)
 ## 题目描述
 给 `n` 个城市(从 `1` 到 `n`)，城市和无向道路`成本`之间的关系为3元组 `[A, B, C]`（在城市 `A` 和城市 `B` 之间有一条路，成本是 `C`）我们需要从1开始找到的旅行所有城市的付出最小的成本。
 ### 样例说明
 
 ### 参考代码
 如果要保证正确性的最优做法。状态压缩动态规划。
```python
class Solution:
    """
    @param n: an integer,denote the number of cities
    @param roads: a list of three-tuples,denote the road between cities
    @return: return the minimum cost to travel all cities
    """
    def minCost(self, n, roads):
        graph = self.construct_graph(roads, n)
        state_size = 1 << n
        f = [
            [float('inf')] * (n + 1)
            for _ in range(state_size)
        ]
        f[1][1] = 0
        for state in range(state_size):
            for i in range(2, n + 1):
                if state & (1 << (i - 1)) == 0:
                    continue
                prev_state = state ^ (1 << (i - 1))
                for j in range(1, n + 1):
                    if prev_state & (1 << (j - 1)) == 0:
                        continue
                    f[state][i] = min(f[state][i], f[prev_state][j] + graph[j][i])
        return min(f[state_size - 1])
        
    def construct_graph(self, roads, n):
        graph = {
            i: {j: float('inf') for j in range(1, n + 1)}
            for i in range(1, n + 1)
        }
        for a, b, c in roads:
            graph[a][b] = min(graph[a][b], c)
            graph[b][a] = min(graph[b][a], c)
        return graph
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
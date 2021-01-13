# 访问所有节点的最短路径
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/shortest-path-visiting-all-nodes/?utm_source=sc-github-wzz)
 ## 题目描述
 给出 `graph` 为有 N 个节点（编号为 `0, 1, 2, ..., N-1`）的无向连通图。 

`graph.length = N`，且只有节点 `i` 和 `j` 连通时，`j != i` 在列表 `graph[i]` 中恰好出现一次。

返回能够访问所有节点的最短路径的长度。你可以在任一节点开始和停止，也可以多次重访节点，并且可以重用边。
 ### 样例说明
 **样例 1:**
```
输入：graph = [[1,2,3],[0],[0],[0]]
输出：4
解释：
一个可能的路径为 [1,0,2,0,3]
```
**样例 2:**
```
输入：graph = [[1],[0,2,4],[1,3,4],[2],[1,2]]
输出：4
解释：
一个可能的路径为 [0,1,4,2,3]
```
 ### 参考代码
 注意题目中的节点个数是 <= 12 的，这是突破口。
可以使用状态压缩的方式记录有哪些点被访问过了。
存在 BFS Queue 中的是一个二元组 `<visited, stop_at>`

1. visited 可以理解为是一个 boolean 数组，但是为了更方便查询，我们用二进制的方式来表示 visited。
也就是说，如果所有点都没有被访问过，visited = 0，如果只访问了标号0和2的点，那么 visited = (101)2 = 5
每次访问一个新的点只需要让 `visited | 1 << node` 即可算出新的 visited。
2. stop_at 记录的是访问了 visited 这些点以后，停在哪儿了。
```python
from collections import deque


class Solution:
    def shortestPathLength(self, graph: List[List[int]]) -> int:
        queue = deque([])
        distance = {}
        n = len(graph)
        for start in range(n):
            state = (1 << start, start)
            queue.append(state)
            distance[state] = 0
            
        while queue:
            visited, stop_at = queue.popleft()
            for neighbor in graph[stop_at]:
                _visited = visited | (1 << neighbor)
                if (_visited, neighbor) in distance:
                    continue
                queue.append((_visited, neighbor))
                distance[(_visited, neighbor)] = distance[(visited, stop_at)] + 1
                if _visited == (1 << n) - 1:
                    return distance[(_visited, neighbor)]
                
        return 0
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
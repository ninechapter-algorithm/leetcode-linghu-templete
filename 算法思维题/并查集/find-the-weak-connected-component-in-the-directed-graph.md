# 找出有向图中的弱连通分量
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-the-weak-connected-component-in-the-directed-graph/?utm_source=sc-github-wzz)
 ## 题目描述
 请找出有向图中弱连通分量。图中的每个节点包含 1 个标签和1 个相邻节点列表。（有向图的弱连通分量是任意两点均有有向边相连的极大子图）
 ### 样例说明
 **样例 1:**

```
输入: {1,2,4#2,4#3,5#4#5#6,5}
输出: [[1,2,4],[3,5,6]]
解释: 
  1----->2    3-->5
   \     |        ^
    \    |        |
     \   |        6
      \  v
       ->4
```

**样例 2:**

```
输入: {1,2#2,3#3,1}
输出: [[1,2,3]]
```
 ### 参考代码
 可以把每条有向边看成无向边, 就等同于在无向图中寻找联通块. 

两种做法: 1. BFS/DFS 2. 并查集 (但由于输入数据是有向边, 所以使用并查集更合适, 否则还需要先把有向边转换成无向边)

可以参考 [431. 找无向图的连通块](https://www.lintcode.com/problem/connected-component-in-undirected-graph/description)
```python
# Definition for a directed graph node
# class DirectedGraphNode:
#     def __init__(self, x):
#         self.label = x
#         self.neighbors = []
class Solution:
    def __init__(self):
        self.f = {}

    def merge(self, x, y):
        x = self.find(x)
        y = self.find(y)
        if x != y:
            self.f[x] = y

    def find(self, x):
        if self.f[x] == x:
            return x
        
        self.f[x] = self.find(self.f[x])
        return self.f[x]

    # @param {DirectedGraphNode[]} nodes a array of directed graph node
    # @return {int[][]} a connected set of a directed graph
    def connectedSet2(self, nodes):
        for node in nodes:
            self.f[node.label] = node.label

        for node in nodes:
            for nei in node.neighbors:
                self.merge(node.label, nei.label)

        result = []
        g = {}
        cnt = 0

        for node in nodes:
            x = self.find(node.label)
            if not x in g:
                cnt += 1
                g[x] = cnt
            
            if len(result) < cnt:
                result.append([])
        
            result[g[x] - 1].append(node.label)

        return result
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
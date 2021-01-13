# 飞行棋 I
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/modern-ludo-i/?utm_source=sc-github-wzz)
 ## 题目描述
 有一个一维的棋盘，起点在棋盘的最左侧，终点在棋盘的最右侧，棋盘上有几个位置是跟其他的位置相连的，即如果A与B相连，则当棋子落在位置A时, 你可以选择是否不投骰子，直接移动棋子从A到B。并且这个连接是单向的，即不能从B移动到A，现在给定这个棋盘的长度`length`和位置的相连情况`connections`，你有一个六面的骰子(点数1-6)，最少需要丢几次才能到达终点。
 ### 样例说明
 **样例1**

```
输入: length = 10 和 connections = [[2, 10]]
输出: 1
解释: 
1->2 (投骰子)
2->10(直接相连)
```

**样例2**

```
输入: length = 15 和 connections = [[2, 8],[6, 9]]
输出: 2
解释: 
1->6 (投骰子)
6->9 (直接相连)
9->15(投骰子)
```

 ### 参考代码
 两个队列交替
```
[[python]]
class Solution:
    def modernLudo(self, length, connections):
        graph = self.build_graph(length, connections)
        
        queue = [1]
        distance = {1: 0}
        while queue:
            next_queue = []
            for node in queue:
                for direct_node in graph[node]:
                    if direct_node in distance:
                        continue
                    distance[direct_node] = distance[node]
                    queue.append(direct_node)
            for node in queue:
                for next_node in range(node + 1, min(node + 7, length + 1)):
                    if next_node in distance:
                        continue
                    distance[next_node] = distance[node] + 1
                    next_queue.append(next_node)
            queue = next_queue
                
        return distance[length]

    def build_graph(self, length, connections):
        graph = {
            i: set()
            for i in range(1, length + 1)
        }
        for a, b in connections:
            graph[a].add(b)
        return graph
[[java]]
public class Solution {
    public int modernLudo(int length, int[][] connections) {
        Map<Integer, Set<Integer>> graph = buildGraph(length, connections);
        
        List<Integer> queue = new ArrayList<>();
        queue.add(1);
        Map<Integer, Integer> distance = new HashMap<>();
        distance.put(1, 0);
        
        while (!queue.isEmpty()) {
            List<Integer> nextQueue = new ArrayList<>();
            for (int i = 0; i < queue.size(); i++) {
                int node = queue.get(i);
                for (int directNode: graph.get(node)) {
                    if (distance.containsKey(directNode)) {
                        continue;
                    }
                    distance.put(directNode, distance.get(node));
                    queue.add(directNode);
                }
            }
            for (int i = 0; i < queue.size(); i++) {
                int node = queue.get(i);
                int limit = Math.min(node + 7, length + 1);
                for (int nextNode = node + 1; nextNode < limit; nextNode++) {
                    if (distance.containsKey(nextNode)) {
                        continue;
                    }
                    distance.put(nextNode, distance.get(node) + 1);
                    nextQueue.add(nextNode);
                }
            }
            queue = nextQueue;
        }
        
        return distance.get(length);
    }
    
    private Map<Integer, Set<Integer>> buildGraph(int length, int[][] connections) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 1; i <= length; i++) {
            graph.put(i, new HashSet<>());
        }
        for (int i = 0; i < connections.length; i++) {
            int from = connections[i][0];
            int to = connections[i][1];
            graph.get(from).add(to);
        }
        return graph;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
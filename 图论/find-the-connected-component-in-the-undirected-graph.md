# 找无向图的连通块
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-the-connected-component-in-the-undirected-graph/?utm_source=sc-github-wzz)
 ## 题目描述
 找出无向图中所有的连通块。

图中的每个节点包含一个label属性和一个邻接点的列表。

（一个无向图的连通块是一个子图，其中任意两个顶点通过路径相连，且不与整个图中的其它顶点相连。）

你需要返回 label 集合的列表.
 ### 样例说明
 
 ### 参考代码
 > 两种方法, BFS/DFS和并查集

BFS/DFS方法:

一次遍历可遍历一整个连通块, 所以标记好每个点是否访问过, 只遍历未访问过的点, 计数直到所有的点都被访问过, 开始过多少次遍历即可.

---

并查集方法(见C++):

假设有 n 个节点. 初始有 n 个集合, 枚举所有的边, 每次把边的两端点所在集合合并, 最后剩余集合的个数即是连通块个数. 一个集合内部的节点即是一个连通块内的节点.
```java
/**
 * Definition for Undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    public List<List<Integer>> connectedSet(List<UndirectedGraphNode> nodes) {
        List<List<Integer>> result = new ArrayList<>();
        if (nodes == null) {
            return result;
        }
        Set<UndirectedGraphNode> visited = new HashSet<>();
        for (UndirectedGraphNode curr : nodes) {
            if (!visited.contains(curr)) {
                findConnect(curr, result, visited);
            }
        }
        return result;
    }
    public void findConnect(UndirectedGraphNode node, List<List<Integer>> result, Set<UndirectedGraphNode> visited) {
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        queue.offer(node);
        visited.add(node);
        List<Integer> list = new ArrayList<>();
        
        while (!queue.isEmpty()) {
            UndirectedGraphNode curr = queue.poll();
            list.add(curr.label);
            for (UndirectedGraphNode next : curr.neighbors) {
                if (!visited.contains(next)){
                    queue.offer(next);
                    visited.add(next);
                }
            }
        }
        Collections.sort(list);
        result.add(list);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
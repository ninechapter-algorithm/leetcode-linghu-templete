# 序列重构
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sequence-reconstruction/?utm_source=sc-github-wzz)
 ## 题目描述
 判断是否序列 `org` 能唯一地由 `seqs`重构得出. `org`是一个由从1到n的正整数排列而成的序列，$1 \leq n \leq 10^4$。 重构表示组合成`seqs`的一个最短的父序列 (意思是，一个最短的序列使得所有 `seqs`里的序列都是它的子序列). 
判断是否有且仅有一个能从 `seqs`重构出来的序列，并且这个序列是`org`。
 ### 样例说明
 例1:
```
输入:org = [1,2,3], seqs = [[1,2],[1,3]]
输出: false
解释:
[1,2,3] 并不是唯一可以被重构出的序列，还可以重构出 [1,3,2]
```
例2:
```
输入: org = [1,2,3], seqs = [[1,2]]
输出: false
解释:
能重构出的序列只有 [1,2].
```
例3:
```
输入: org = [1,2,3], seqs = [[1,2],[1,3],[2,3]]
输出: true
解释:
序列 [1,2], [1,3], 和 [2,3] 可以唯一重构出 [1,2,3].
```
例4:
```
输入:org = [4,1,5,2,6,3], seqs = [[5,2,6,3],[4,1,5,2]]
输出:true
```

 ### 参考代码
 九章算法班里讲过的拓扑排序喽
只要保证 queue 里最多同时只有一个元素即可。
所以这是 queue 用 list 然后每次 pop 也可以，反正只有一个数。
```
[[python]]
class Solution:
    """
    @param org: a permutation of the integers from 1 to n
    @param seqs: a list of sequences
    @return: true if it can be reconstructed only one or false
    """
    def sequenceReconstruction(self, org, seqs):
        graph = self.build_graph(seqs)
        topo_order = self.topological_sort(graph)
        return topo_order == org
            
    def build_graph(self, seqs):
        # initialize graph
        graph = {}
        for seq in seqs:
            for node in seq:
                if node not in graph:
                    graph[node] = set()
        
        for seq in seqs:
            for i in range(1, len(seq)):
                graph[seq[i - 1]].add(seq[i])

        return graph
    
    def get_indegrees(self, graph):
        indegrees = {
            node: 0
            for node in graph
        }
        
        for node in graph:
            for neighbor in graph[node]:
                indegrees[neighbor] += 1
                
        return indegrees
        
    def topological_sort(self, graph):
        indegrees = self.get_indegrees(graph)
        
        queue = []
        for node in graph:
            if indegrees[node] == 0:
                queue.append(node)
        
        topo_order = []
        while queue:
            if len(queue) > 1:
                # there must exist more than one topo orders
                return None
                
            node = queue.pop()
            topo_order.append(node)
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    queue.append(neighbor)
                    
        if len(topo_order) == len(graph):
            return topo_order
            
        return None
[[java]]
public class Solution {
    /**
     * @param org: a permutation of the integers from 1 to n
     * @param seqs: a list of sequences
     * @return: true if it can be reconstructed only one or false
     */
    public boolean sequenceReconstruction(int[] org, int[][] seqs) {
        Map<Integer, Set<Integer>> graph = buildGraph(seqs);
        List<Integer> topoOrder = getTopoOrder(graph);
        
        if (topoOrder == null || topoOrder.size() != org.length) {
            return false;
        }
        for (int i = 0; i < org.length; i++) {
            if (org[i] != topoOrder.get(i)) {
                return false;
            }
        }
        return true;
    }
    
    private Map<Integer, Set<Integer>> buildGraph(int[][] seqs) {
        Map<Integer, Set<Integer>> graph = new HashMap();
        for (int[] seq : seqs) {
            for (int i = 0; i < seq.length; i++) {
                if (!graph.containsKey(seq[i])) {
                    graph.put(seq[i], new HashSet<Integer>());
                }
            }
        }
        for (int[] seq : seqs) {
            for (int i = 1; i < seq.length; i++) {
                graph.get(seq[i - 1]).add(seq[i]);
            }
        }
        return graph;
    }
    
    private Map<Integer, Integer> getIndegrees(Map<Integer, Set<Integer>> graph) {
        Map<Integer, Integer> indegrees = new HashMap();
        for (Integer node : graph.keySet()) {
            indegrees.put(node, 0);
        }
        for (Integer node : graph.keySet()) {
            for (Integer neighbor : graph.get(node)) {
                indegrees.put(neighbor, indegrees.get(neighbor) + 1);
            }
        }
        return indegrees;
    }
    
    private List<Integer> getTopoOrder(Map<Integer, Set<Integer>> graph) {
        Map<Integer, Integer> indegrees = getIndegrees(graph);
        Queue<Integer> queue = new LinkedList();
        List<Integer> topoOrder = new ArrayList();
        
        for (Integer node : graph.keySet()) {
            if (indegrees.get(node) == 0) {
                queue.offer(node);
                topoOrder.add(node);
            }
        }
        
        while (!queue.isEmpty()) {
            if (queue.size() > 1) {
                return null;
            }
            
            Integer node = queue.poll();
            for (Integer neighbor : graph.get(node)) {
                indegrees.put(neighbor, indegrees.get(neighbor) - 1);
                if (indegrees.get(neighbor) == 0) {
                    queue.offer(neighbor);
                    topoOrder.add(neighbor);
                }
            }
        }
        
        if (graph.size() == topoOrder.size()) {
            return topoOrder;
        }
        
        return null;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
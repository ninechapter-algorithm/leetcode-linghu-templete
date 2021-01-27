# 树上最长路径
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-path-on-the-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给出由`n`个结点，`n-1`条边组成的一棵树。求这棵树中距离最远的两个结点之间的距离。
给出三个大小为`n-1`的数组`starts`,`ends`,`lens`,表示第`i`条边是从`starts[i]`连向`ends[i]`，长度为`lens[i]`的无向边。
 ### 样例说明
 **Example 1:**
```
Input：n=5,starts=[0,0,2,2],ends=[1,2,3,4],lens=[1,2,5,6]
Output：11
解释:
(3→2→4)这条路径长度为`11`，当然(4→2→3)也是一样的。
```

**Example 2:**
```
Input：n=5,starts=[0,0,2,2],ends=[1,2,3,4],lens=[5,2,5,6]
Output：13
解释:
(1→0→2→4)这条路径长度为`13`，当然(4→2→0→1)也是一样的。
```
 ### 参考代码
 ```
[[python]]
class Solution:
    """
    @param n: The number of nodes
    @param starts: One point of the edge
    @param ends: Another point of the edge
    @param lens: The length of the edge
    @return: Return the length of longest path on the tree.
    """
    def longestPath(self, n, starts, ends, lens):
        graph = self.build_graph(starts, ends, lens)
        bfs_order = self.get_bfs_order(graph)
        return self.find_longest_path(bfs_order, graph)
        
    def build_graph(self, starts, ends, lens):
        n = len(starts) + 1
        graph = {i: {} for i in range(n)}
        for i in range(n - 1):
            graph[starts[i]][ends[i]] = lens[i]
            graph[ends[i]][starts[i]] = lens[i]
        return graph
        
    def get_bfs_order(self, graph):        
        n = len(graph)
        queue, start = [0], 0
        visited = set([0])
        while start < len(queue):
            node = queue[start]
            for neighbor in graph[node]:
                if neighbor in visited:
                    continue
                visited.add(neighbor)
                queue.append(neighbor)
            start += 1
        
        return queue
        
    def find_longest_path(self, bfs_order, graph):
        longest_path_to_leaf = {}
        longest_path = -float('inf')
        for node in reversed(bfs_order):
            max_path, second_max_path = -float('inf'), -float('inf')
            for neighbor in graph[node]:
                # if neighbor is parent
                if neighbor not in longest_path_to_leaf:
                    continue
                if graph[node][neighbor] + longest_path_to_leaf[neighbor] > max_path:
                    second_max_path = max_path
                    max_path = graph[node][neighbor] + longest_path_to_leaf[neighbor]
                elif graph[node][neighbor] + longest_path_to_leaf[neighbor] > second_max_path:
                    second_max_path = graph[node][neighbor] + longest_path_to_leaf[neighbor]
            # if max_path == -float('inf') that means node is a leaf
            longest_path_to_leaf[node] = max(max_path, 0)
            longest_path = max(longest_path, longest_path_to_leaf[node])
            if second_max_path != -float('inf'):
                longest_path = max(longest_path, max_path + second_max_path)
        return longest_path
[[java]]
public class Solution {
    /**
     * @param n: The number of nodes
     * @param starts: One point of the edge
     * @param ends: Another point of the edge
     * @param lens: The length of the edge
     * @return: Return the length of longest path on the tree.
     */
    public int longestPath(int n, int[] starts, int[] ends, int[] lens) {
        Map<Integer, Map<Integer, Integer>> graph = buildGraph(starts, ends, lens);
        List<Integer> bfsOrder = getBfsOrder(graph);
        return findLongestPath(bfsOrder, graph);
    }
    
    private Map<Integer, Map<Integer, Integer>> buildGraph(int[] starts, int[] ends, int[] lens) {
        int n = starts.length + 1;
        Map<Integer, Map<Integer, Integer>> graph = new HashMap<>();
        for (int i = 0; i < n - 1; i++) {
            if (!graph.containsKey(starts[i])) {
                graph.put(starts[i], new HashMap<Integer, Integer>());
            }
            if (!graph.containsKey(ends[i])) {
                graph.put(ends[i], new HashMap<Integer, Integer>());
            }
            graph.get(starts[i]).put(ends[i], lens[i]);
            graph.get(ends[i]).put(starts[i], lens[i]);
        }
        return graph;
    }
    
    private List<Integer> getBfsOrder(Map<Integer, Map<Integer, Integer>> graph) {
        int n = graph.size();
        List<Integer> queue = new ArrayList<>();
        int start = 0;
        Set<Integer> visited = new HashSet<>();
        queue.add(0);
        visited.add(0);
        
        while (start < queue.size()) {
            int node = queue.get(start);
            for (int neighbor: graph.getOrDefault(node, new HashMap<>()).keySet()) {
                if (visited.contains(neighbor)) {
                    continue;
                }
                visited.add(neighbor);
                queue.add(neighbor);
            }
            start++;
        }
        
        return queue;
    }
    
    private int findLongestPath(List<Integer> bfsOrder, Map<Integer, Map<Integer, Integer>> graph) {
        Map<Integer, Integer> longestPathToLeaf = new HashMap<>();
        int longestPath = Integer.MIN_VALUE;
        for (int i = bfsOrder.size() - 1; i >= 0; i--) {
            int node = bfsOrder.get(i);
            int maxPath = Integer.MIN_VALUE, secondMaxPath = Integer.MIN_VALUE;
            for (int neighbor: graph.getOrDefault(node, new HashMap<>()).keySet()) {
                // if neighbor is parent
                if (!longestPathToLeaf.containsKey(neighbor)) {
                    continue;
                }
                if (graph.get(node).get(neighbor) + longestPathToLeaf.get(neighbor) > maxPath) {
                    secondMaxPath = maxPath;
                    maxPath = graph.get(node).get(neighbor) + longestPathToLeaf.get(neighbor);
                } else if (graph.get(node).get(neighbor) + longestPathToLeaf.get(neighbor) > secondMaxPath) {
                    secondMaxPath = graph.get(node).get(neighbor) + longestPathToLeaf.get(neighbor);
                }
            }
            // if maxPath == Integer.MIN_VALUE that means node is a leaf
            longestPathToLeaf.put(node, Math.max(maxPath, 0));
            longestPath = Math.max(longestPath, longestPathToLeaf.get(node));
            if (secondMaxPath != Integer.MIN_VALUE) {
                longestPath = Math.max(longestPath, maxPath + secondMaxPath);
            }
        }
        return longestPath;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
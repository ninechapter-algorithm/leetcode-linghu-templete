# 外星人词典
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/alien-dictionary/?utm_source=sc-github-wzz)
 ## 题目描述
 有一种新的使用拉丁字母的外来语言。但是，你不知道字母之间的顺序。你会从词典中收到一个**非空的**单词列表，其中的单词**在这种新语言的规则下按字典顺序排序**。请推导出这种语言的字母顺序。
 ### 样例说明
 **样例 1:**
```
输入：["wrt","wrf","er","ett","rftt"]
输出："wertf"
解释：
从 "wrt"和"wrf" ,我们可以得到 't'<'f'
从 "wrt"和"er" ,我们可以得到'w'<'e'
从 "er"和"ett" ,我们可以得到 get 'r'<'t'
从 "ett"和"rftt" ,我们可以得到 'e'<'r'
所以返回 "wertf"

```


**样例 2:**
```
输入：["z","x"]
输出："zx"
解释：
从 "z" 和 "x"，我们可以得到 'z' < 'x'
所以返回"zx"
```
 ### 参考代码
 使用拓扑排序算法。
这个版本的实现当中，无需假设所有字母为小写字母。
```
[[java]]
class Solution {
    public String alienOrder(String[] words) {
        Map<Character, Set<Character>> graph = constructGraph(words);
        if (graph == null) {
            return "";
        }
        return topologicalSorting(graph);
    }
    
        
    private Map<Character, Set<Character>> constructGraph(String[] words) {
        Map<Character, Set<Character>> graph = new HashMap<>();
        
        // create nodes
        for (int i = 0; i < words.length; i++) {
            for (int j = 0; j < words[i].length(); j++) {
                char c = words[i].charAt(j);
                if (!graph.containsKey(c)) {
                    graph.put(c, new HashSet<Character>());
                }
            }
        }
        
        // create edges
        for (int i = 0; i < words.length - 1; i++) {
            int index = 0;
            while (index < words[i].length() && index < words[i + 1].length()) {
                if (words[i].charAt(index) != words[i + 1].charAt(index)) {
                    graph.get(words[i].charAt(index)).add(words[i + 1].charAt(index));
                    break;
                }
                index++;
            }
            if (index == Math.min(words[i].length(), words[i + 1].length())) {
                if (words[i].length() > words[i + 1].length()) {
                    return null;
                }
            }
        }

        return graph;
    }
    
    private Map<Character, Integer> getIndegree(Map<Character, Set<Character>> graph) {
        Map<Character, Integer> indegree = new HashMap<>();
        for (Character u : graph.keySet()) {
            indegree.put(u, 0);
        }
        
        for (Character u : graph.keySet()) {
            for (Character v : graph.get(u)) {
                indegree.put(v, indegree.get(v) + 1);
            }
        }     
        
        return indegree;
    }

    private String topologicalSorting(Map<Character, Set<Character>> graph) {
        // as we should return the topo order with lexicographical order
        // we should use PriorityQueue instead of a FIFO Queue
        Map<Character, Integer> indegree = getIndegree(graph);
        Queue<Character> queue = new PriorityQueue<>();
        
        for (Character u : indegree.keySet()) {
            if (indegree.get(u) == 0) {
                queue.offer(u);
            }
        }
        
        StringBuilder sb = new StringBuilder();
        while (!queue.isEmpty()) {
            Character head = queue.poll();
            sb.append(head);
            for (Character neighbor : graph.get(head)) {
                indegree.put(neighbor, indegree.get(neighbor) - 1);
                if (indegree.get(neighbor) == 0) {
                    queue.offer(neighbor);
                }
            }
        }
        if (sb.length() != indegree.size()) {
            return "";
        }
        return sb.toString();
    }
}

[[python]]
"""
before looking into this part of code
you should know how to use bfs algorithm to do topological sorting
if you don't know, please google it first or join us at 九章算法班.
"""

from heapq import heappush, heappop, heapify

class Solution:
    """
    @param words: a list of words
    @return: a string which is correct order
    """
    def alienOrder(self, words):
        graph = self.build_graph(words)
        if not graph:
            return ""
        return self.topological_sort(graph)
        
    def build_graph(self, words):
        # key is node, value is neighbors
        graph = {}

        # initialize graph
        for word in words:
            for c in word:
                if c not in graph:
                    graph[c] = set() 

        # add edges        
        n = len(words)
        for i in range(n - 1):
            for j in range(min(len(words[i]), len(words[i + 1]))):
                if words[i][j] != words[i + 1][j]:
                    graph[words[i][j]].add(words[i + 1][j])
                    break
                if j == min(len(words[i]), len(words[i + 1])) - 1:
                    if len(words[i]) > len(words[i + 1]):
                        return None
                
        return graph

    def topological_sort(self, graph):        
        # initialize indegree 
        indegree = {
            node: 0
            for node in graph
        }
        
        # calculate indegree
        for node in graph:
            for neighbor in graph[node]:
                indegree[neighbor] = indegree[neighbor] + 1
        
        # use heapq instead of regular queue so that we can get the 
        # smallest lexicographical order
        queue = [node for node in graph if indegree[node] == 0]
        heapify(queue)
        
        # regular bfs algorithm to do topological sorting
        topo_order = ""
        while queue:
            node = heappop(queue)
            topo_order += node
            for neighbor in graph[node]:
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    heappush(queue, neighbor)
            
        # if all nodes popped
        if len(topo_order) == len(graph):
            return topo_order
        
        return ""

[[c++]]
class Solution {
public:
    /**
     * @param words: a list of words
     * @return: a string which is correct order
     */
    string alienOrder(vector<string>& words) {
        map<char, set<char> > graph = constructGraph(words);
        if (!graph.size()) {
            return "";
        }

        return topologicalSorting(graph);
    }

    map<char, set<char> > constructGraph(vector<string>& words) {
        map<char, set<char> > graph;
        // create nodes
        for (int i = 0; i < words.size(); i++) {
            for (int j = 0; j < words[i].size(); j++) {
                char c = words[i][j];
                if (graph.find(c) == graph.end()) {
                    set<char> temp;
                    graph[c] = temp;
                }
            }
        }

        // create edges
        for (int i = 0; i < words.size() - 1; i++) {
            int index = 0;
            while (index < words[i].size() && index < words[i + 1].size()) {
                if (words[i][index] != words[i + 1][index]) {
                    graph[words[i][index]].insert(words[i + 1][index]);
                    break;
                }
                index++;
            }
            if (index == min(words[i].size(), words[i + 1].size())) {
                if (words[i].size() > words[i + 1].size()) {
                    return map<char, set<char> >();
                }
            }
        }

        return graph;
    }

    map<char, int> getIndegree(map<char, set<char> >& graph) {
        map<char, int> indegree;
        map<char, set<char> >::iterator iter;
        iter = graph.begin();
        while (iter != graph.end()) {
            indegree[iter->first] = 0;
            iter++;
        }
        
        iter = graph.begin();
        while (iter != graph.end()) {
            set<char>::iterator _iter = (iter->second).begin();
            while (_iter != (iter->second).end()) {
                indegree[*_iter] = indegree[*_iter] + 1;
                _iter++;
            }
            iter++;
        }

        return indegree;
    }
    
    string topologicalSorting(map<char, set<char> > graph) {
        map<char, int> indegree = getIndegree(graph);

        priority_queue<char, vector<char>, greater<char> > Q;

        map<char, int>::iterator iter;
        iter = indegree.begin();
        while (iter != indegree.end()) {
            if (indegree[iter->first] == 0) {
                Q.push(iter->first);
            }
            iter++;
        }

        string s = "";
        while (Q.size()) {
            char head = Q.top();
            Q.pop();
            s += head;
            set<char>::iterator iter;
            iter = graph[head].begin();
            while (iter != graph[head].end()) {
                char neighbor = *iter;
                indegree[neighbor] -= 1;
                if (indegree[neighbor] == 0) {
                    Q.push(neighbor);
                }
                iter++;
            }
        }
        
        if (s.size() != indegree.size()) {
            return "";
        }
        return s;
    }

};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
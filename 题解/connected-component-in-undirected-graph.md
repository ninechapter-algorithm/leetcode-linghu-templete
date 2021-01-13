# 找无向图的连通块
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/connected-component-in-undirected-graph/?utm_source=sc-github-wzz)
 ## 题目描述
 找出无向图中所有的连通块。

图中的每个节点包含一个label属性和一个邻接点的列表。

（一个无向图的连通块是一个子图，其中任意两个顶点通过路径相连，且不与整个图中的其它顶点相连。）

你需要返回 label 集合的列表.
 ### 样例说明
 **样例 1:**

```
输入: {1,2,4#2,1,4#3,5#4,1,2#5,3}
输出: [[1,2,4],[3,5]]
解释: 

  1------2  3
   \     |  | 
    \    |  |
     \   |  |
      \  |  |
        4   5
```

**样例 2:**

```
输入: {1,2#2,1}
输出: [[1,2]]
解释:

  1--2

```
 ### 参考代码
 无向图连通块, 可以使用BFS或者并查集union find求解                         .
```java
/**
  * 本代码由九章算法编辑提供。版权所有，转发请注明出处。
  * - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
  * - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，Big Data 项目实战班，
  * - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code
  */ 

// bfs 方法
/**
 * Definition for Undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param nodes a array of Undirected graph node
     * @return a connected set of a Undirected graph
     */
    public List<List<Integer>> connectedSet(List<UndirectedGraphNode> nodes) {
        // Write your code here
        
        Map<UndirectedGraphNode, Boolean> visited = new HashMap<>();
        
       for (UndirectedGraphNode node : nodes){
            visited.put(node, false);
       }
        
        List<List<Integer>> result = new ArrayList<>();
        
        for (UndirectedGraphNode node : nodes){
            if (visited.get(node) == false){
                bfs(node, visited, result);
            }
        }
        
        return result;
    }
    
    public void bfs(UndirectedGraphNode node, Map<UndirectedGraphNode, Boolean> visited, List<List<Integer>> result){
        List<Integer>row = new ArrayList<>();
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        visited.put(node, true);
        queue.offer(node);
        while (!queue.isEmpty()){
            UndirectedGraphNode u = queue.poll();
            row.add(u.label);    
            for (UndirectedGraphNode v : u.neighbors){
                if (visited.get(v) == false){
                    visited.put(v, true);
                    queue.offer(v);
                }
            }
        }
        Collections.sort(row);
        result.add(row);
        
    }
}

//------------------------我是分割线--------------------------------------
// 并查集方法
public
class Solution {
    class UnionFind {
        HashMap<Integer, Integer> father = new HashMap<Integer, Integer>();
        UnionFind(HashSet<Integer> hashSet)
        {
            for (Integer now : hashSet) {
                father.put(now, now);
            }
        }
        int find(int x)
        {
            int parent = father.get(x);
            while (parent != father.get(parent)) {
                parent = father.get(parent);
            }
            return parent;
        }
        int compressed_find(int x)
        {
            int parent = father.get(x);
            while (parent != father.get(parent)) {
                parent = father.get(parent);
            }
            int next;
            while (x != father.get(x)) {
                next = father.get(x);
                father.put(x, parent);
                x = next;
            }
            return parent;
        }

        void union(int x, int y)
        {
            int fa_x = find(x);
            int fa_y = find(y);
            if (fa_x != fa_y)
                father.put(fa_x, fa_y);
        }
    }
    
    List<List<Integer> > print(HashSet<Integer> hashSet, UnionFind uf, int n) {
        List<List<Integer> > ans = new ArrayList<List<Integer> >();
        HashMap<Integer, List<Integer> > hashMap = new HashMap<Integer, List<Integer> >();
        for (int i : hashSet) {
            int fa = uf.find(i);
            if (!hashMap.containsKey(fa)) {
                hashMap.put(fa, new ArrayList<Integer>());
            }
            List<Integer> now = hashMap.get(fa);
            now.add(i);
            hashMap.put(fa, now);
        }
        for (List<Integer> now : hashMap.values()) {
            Collections.sort(now);
            ans.add(now);
        }
        return ans;
    }

public
    List<List<Integer> > connectedSet(List<UndirectedGraphNode> nodes)
    {
        // Write your code here

        HashSet<Integer> hashSet = new HashSet<Integer>();
        for (UndirectedGraphNode now : nodes) {
            hashSet.add(now.label);
            for (UndirectedGraphNode neighbour : now.neighbors) {
                hashSet.add(neighbour.label);
            }
        }
        UnionFind uf = new UnionFind(hashSet);

        for (UndirectedGraphNode now : nodes) {

            for (UndirectedGraphNode neighbour : now.neighbors) {
                int fnow = uf.find(now.label);
                int fneighbour = uf.find(neighbour.label);
                if (fnow != fneighbour) {
                    uf.union(now.label, neighbour.label);
                }
            }
        }

        return print(hashSet, uf, nodes.size());
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
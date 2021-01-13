# 六度问题
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/six-degrees/?utm_source=sc-github-wzz)
 ## 题目描述
 六度分离是一个哲学问题，说的是每个人每个东西可以通过六步或者更少的步数建立联系。

现在给你一个友谊关系，查询两个人可以通过几步相连，如果不相连返回 `-1`
 ### 样例说明
 **样例1**

```
输入: {1,2,3#2,1,4#3,1,4#4,2,3} 和 s = 1, t = 4 
输出: 2
解释:
    1------2-----4
     \          /
      \        /
       \--3--/
```

**样例2**

```
输入: {1#2,4#3,4#4,2,3} 和 s = 1, t = 4
输出: -1
解释:
    1      2-----4
                 /
               /
              3
```
 ### 参考代码
 直接用bfs进行搜索，找答案
```java
/**
 * Definition for Undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x;
 *         neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */
public class Solution {
    /**
     * @param graph a list of Undirected graph node
     * @param s, t two Undirected graph nodes
     * @return an integer
     */
    public int sixDegrees(List<UndirectedGraphNode> graph,
                          UndirectedGraphNode s,
                          UndirectedGraphNode t) {
        // Write your code here
        if (s == t)
            return 0;

        Map<UndirectedGraphNode, Integer> visited = new HashMap<UndirectedGraphNode, Integer>();
        Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
        
        queue.offer(s);
        visited.put(s, 0);
        while (!queue.isEmpty()) {
            UndirectedGraphNode node = queue.poll();
            int step = visited.get(node);
            for (int i = 0; i < node.neighbors.size(); i++) {
                if (visited.containsKey(node.neighbors.get(i))) {
                    continue;
                }
                visited.put(node.neighbors.get(i), step + 1);
                queue.offer(node.neighbors.get(i));
                if (node.neighbors.get(i) == t) {
                    return step + 1;
                }
            }
        }
        
        return -1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
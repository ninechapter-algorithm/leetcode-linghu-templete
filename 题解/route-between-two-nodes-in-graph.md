# 图中两个点之间的路线
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/route-between-two-nodes-in-graph/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一张有向图，设计一个算法判断两个点 `s` 与 `t` 之间是否存在路线。
 ### 样例说明
 如下图:
```
	A----->B----->C
	 \     |
	  \    |
	   \   |
	    \  v
	     ->D----->E
			 
样例 1:
输入:s = B and t = E,
输出:true

样例 2:
输入:s = D and t = C,
输出:false
```
 ### 参考代码
 ```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */
public class Solution {
   /**
     * @param graph: A list of Directed graph node
     * @param s: the starting Directed graph node
     * @param t: the terminal Directed graph node
     * @return: a boolean value
     */
    public boolean hasRoute(ArrayList<DirectedGraphNode> graph,
                                 DirectedGraphNode s, DirectedGraphNode t) {
        if (s == t)
            return true;

        HashSet<DirectedGraphNode> visited = new HashSet<DirectedGraphNode>();
        Queue<DirectedGraphNode> queue = new LinkedList<DirectedGraphNode>();
        
        queue.offer(s);
        visited.add(s);
        while (!queue.isEmpty()) {
            DirectedGraphNode node = queue.poll();
            for (int i = 0; i < node.neighbors.size(); i++) {
                if (visited.contains(node.neighbors.get(i))) {
                    continue;
                }
                visited.add(node.neighbors.get(i));
                queue.offer(node.neighbors.get(i));
                if (node.neighbors.get(i) == t) {
                    return true;
                }
            }
        }
        
        return false;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
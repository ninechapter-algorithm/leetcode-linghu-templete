# 克隆图
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/clone-graph/?utm_source=sc-github-wzz)
 ## 题目描述
 克隆一张无向图. 无向图的每个节点包含一个 `label` 和一个列表 `neighbors`. 保证每个节点的 `label` 互不相同.

你的程序需要返回一个经过深度拷贝的新图. 新图和原图具有同样的结构, 并且对新图的任何改动不会对原图造成任何影响.
 ### 样例说明
 **样例1**
```
输入:
{1,2,4#2,1,4#4,1,2}
输出: 
{1,2,4#2,1,4#4,1,2}
解释:
1------2  
 \     |  
  \    |  
   \   |  
    \  |  
      4   
```
 ### 参考代码
 使用宽度优先搜索 BFS 的版本。

第一步：找到所有的点
第二步：复制所有的点，将映射关系存起来
第三步：找到所有的边，复制每一条边
```python
class Solution:
    def cloneGraph(self, node):
        root = node
        if node is None:
            return node
            
        # use bfs algorithm to traverse the graph and get all nodes.
        nodes = self.getNodes(node)
        
        # copy nodes, store the old->new mapping information in a hash map
        mapping = {}
        for node in nodes:
            mapping[node] = UndirectedGraphNode(node.label)
        
        # copy neighbors(edges)
        for node in nodes:
            new_node = mapping[node]
            for neighbor in node.neighbors:
                new_neighbor = mapping[neighbor]
                new_node.neighbors.append(new_neighbor)
        
        return mapping[root]
        
    def getNodes(self, node):
        q = collections.deque([node])
        result = set([node])
        while q:
            head = q.popleft()
            for neighbor in head.neighbors:
                if neighbor not in result:
                    result.add(neighbor)
                    q.append(neighbor)
        return result
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
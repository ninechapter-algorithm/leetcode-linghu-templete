# 连接图
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/connecting-graph/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个图中的`n`个节点, 记为 `1` 到 `n` . 在开始的时候图中没有边。
你需要完成下面两个方法:
1. `connect(a, b)`, 添加连接节点 `a`, `b` 的边.
2. `query(a, b)`, 检验两个节点是否联通
 ### 样例说明
 
 ### 参考代码
 简单并查集实现并和查操作。
```python
class ConnectingGraph:
    """
    @param: n: An integer
    """
    def __init__(self, n):
        self.father = {}
        for i in range(1, n + 1):
            self.father[i] = i

    """
    @param: a: An integer
    @param: b: An integer
    @return: nothing
    """
    def connect(self, a, b):
        self.father[self.find(a)] = self.find(b)

    """
    @param: a: An integer
    @param: b: An integer
    @return: A boolean
    """
    def query(self, a, b):
        return self.find(a) == self.find(b)
        
    def find(self, node):
        path = []
        while self.father[node] != node:
            path.append(node)
            node = self.father[node]
            
        for n in path:
            self.father[n] = node
            
        return node
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
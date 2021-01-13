# 连接图 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/connecting-graph-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个图中的 `n` 个节点, 记为 `1` 到 `n` . 在开始的时候图中没有边.
你需要完成下面两个方法:
1. 	`connect(a, b)`, 添加一条连接节点 a, b的边
2. 	`query()`, 返回图中联通区域个数
 ### 样例说明
 例1:
```
输入:
ConnectingGraph3(5)
query()
connect(1, 2)
query()
connect(2, 4)
query()
connect(1, 4)
query()

输出:[5,4,3,3]

```

例2:
```
输入:
ConnectingGraph3(6)
query()
query()
query()
query()
query()


输出:
[6,6,6,6,6]


```

 ### 参考代码
 并查集。
实时维护区域的个数，即若在某一次合并中两个区域合并成一个，那么数量-1。
```python
class ConnectingGraph3:
    """
    @param: n: An integer
    """
    def __init__(self, n):
        self.size = n
        self.father = {}
        for i in range(1, n + 1):
            self.father[i] = i

    """
    @param: a: An integer
    @param: b: An integer
    @return: nothing
    """
    def connect(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
            self.size -= 1
            
    """
    @return: An integer
    """
    def query(self):
        return self.size

    def find(self, node):
        path = []
        while node != self.father[node]:
            path.append(node)
            node = self.father[node]
        
        for n in path:
            self.father[n] = node
        return node
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
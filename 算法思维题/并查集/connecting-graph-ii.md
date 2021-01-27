# 连接图 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/connecting-graph-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个图中的 `n` 个节点, 记为 `1` 到 `n` .在开始的时候图中没有边.
你需要完成下面两个方法：
1. 	`connect(a, b)`, 添加一条连接节点 a, b的边
2. 	`query(a)`, 返回图中含 `a` 的联通区域内节点个数
 ### 样例说明
 例1:
```
输入:
ConnectingGraph2(5)
query(1)
connect(1, 2)
query(1)
connect(2, 4)
query(1)
connect(1, 4)
query(1)

输出:
[1,2,3,3]


```
例2:
```
输入:
ConnectingGraph2(6)
query(1)
query(2)
query(1)
query(5)
query(1)


输出:
[1,1,1,1,1]


```

 ### 参考代码
 并查集。
同时维护一下个数即可。
```java
public class ConnectingGraph2 { 

    private int[] father = null;
    private int[] size = null;

    private int find(int x) {
        int j, k, fx;
        j = x;
        while (father[j] != j){
            j = father[j];
        }
        
        while (x != j){
            fx = father[x];
            father[x] = j;
            x = fx;
        }
        
        return j;
    }

    public ConnectingGraph2(int n) {
        // initialize your data structure here.
        father = new int[n + 1];
        size = new int[n + 1];
        for (int i = 1; i <= n; ++i) {
            father[i] = i;
            size[i] = 1;
        }
    }

    public void connect(int a, int b) {
        // Write your code here
        int root_a = find(a);
        int root_b = find(b);
        if (root_a != root_b) {
            father[root_a] = root_b;
            size[root_b] += size[root_a];
        }
    }
        
    public int query(int a) {
        // Write your code here
        int root_a = find(a);
        return size[root_a];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
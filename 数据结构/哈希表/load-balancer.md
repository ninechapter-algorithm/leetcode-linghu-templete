# 负载均衡器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/load-balancer/?utm_source=sc-github-wzz)
 ## 题目描述
 为网站实现一个负载均衡器，提供如下的 3 个功能：

1. 添加一台新的服务器到整个集群中 => `add(server_id)`。
2. 从集群中删除一个服务器 => `remove(server_id)`。
3. 在集群中随机（等概率）选择一个有效的服务器 => `pick()`。

最开始时，集群中一台服务器都没有。每次 `pick()` 调用你需要在集群中随机返回一个 `server_id`。
 ### 样例说明
 **样例 1:**
```
输入:
  add(1)
  add(2)
  add(3)
  pick()
  pick()
  pick()
  pick()
  remove(1)
  pick()
  pick()
  pick()
输出:
  1
  2
  1
  3
  2
  3
  3
解释: pick() 的返回值是随机的，也可以是 2 3 3 1 3 2 2 或其他的。
```

**样例 2:**
```
输入:
  add(1)
  add(2)
  remove(1)
  pick()
  pick()
输出:
  2
  2
```

 ### 参考代码
 一种可行的思路是同时使用哈希表和数组.

* `pick()`: 数组中随机选取一个元素可以直接使用随机函数得到一个 \[0, 数组大小-1\] 的整数即可.
* `add(server_id)`: 在数组末尾添加这个`server_id`, 并在哈希表中添加 `server_id` -> 数组下标 的键值映射
* `remove(server_id)`: 利用哈希表得到 `server_id` 的数组下标, 在数组中将它和最末尾的元素交换位置, 然后删除, 并将修改同步到哈希表
```python
class LoadBalancer:
    
    def __init__(self):
        self.server_ids = []
        self.id2index = {}

    # @param {int} server_id add a new server to the cluster 
    # @return nothing
    def add(self, server_id):
        if server_id in self.id2index:
            return
        self.server_ids.append(server_id)
        self.id2index[server_id] = len(self.server_ids) - 1

    # @param {int} server_id remove a bad server from the cluster
    # @return nothing
    def remove(self, server_id):
        if server_id not in self.id2index:
            return
        
        # remove the server_id
        index = self.id2index[server_id]
        del self.id2index[server_id]
        
        # overwrite the one to be removed
        last_server_id = self.server_ids[-1]
        self.id2index[last_server_id] = index
        self.server_ids[index] = last_server_id
        self.server_ids.pop()

    # @return {int} pick a server in the cluster randomly with equal probability
    def pick(self):
        import random
        index = random.randint(0, len(self.server_ids) - 1)
        return self.server_ids[index]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
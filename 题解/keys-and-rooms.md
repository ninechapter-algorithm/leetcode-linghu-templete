# 钥匙和房间
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/keys-and-rooms/?utm_source=sc-github-wzz)
 ## 题目描述
 有 `N` 个房间，开始时你位于 `0` 号房间。每个房间有不同的号码：`0，1，2，...，N-1`，并且房间里可能有一些钥匙能使你进入下一个房间。

在形式上，对于每个房间 `i` 都有一个钥匙列表 `rooms[i]`，每个钥匙 `rooms[i][j]`由 `[0,1，...，N-1]` 中的一个整数表示，其中 `N = rooms.length`。 钥匙 `rooms[i][j] = v` 可以打开编号为 `v` 的房间。

最初，除 `0` 号房间外的其余所有房间都被锁住。

你可以自由地在房间之间来回走动。

如果能进入每个房间返回 `true`，否则返回 `false`。
 ### 样例说明
 **样例 1:**
```
输入: rooms = [[1],[2],[3],[]]
输出: true
解释:  
我们从 0 号房间开始，拿到钥匙 1。
之后我们去 1 号房间，拿到钥匙 2。
然后我们去 2 号房间，拿到钥匙 3。
最后我们去了 3 号房间。
由于我们能够进入每个房间，我们返回 true。
```
**样例 2:**
```
输入: rooms = [[1,3],[3,0,1],[2],[0]]
输出: false
解释: 
我们不能进入 2 号房间。
```
 ### 参考代码
 看看从0出发能否连通所有的点。
找连通性问题用 BFS

```
[[python]]
class Solution:
    """
    @param rooms: a list of keys rooms[i]
    @return: can you enter every room
    """
    def canVisitAllRooms(self, rooms):
        from collections import deque
        queue = deque([0])
        visited = set([0])
        while queue:
            room_id = queue.popleft()
            for next_room_id in rooms[room_id]:
                if next_room_id in visited:
                    continue
                queue.append(next_room_id)
                visited.add(next_room_id)
        return len(visited) == len(rooms)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
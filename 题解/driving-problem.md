# 开车问题
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/driving-problem/?utm_source=sc-github-wzz)
 ## 题目描述
 有一条路长为`L`，宽为`W`，在路中有一些圆形障碍物，半径1，有一辆圆形的车，半径2，问车是否能通过这条路。你可以把路面当成二维坐标上的一个矩形，四个点为`(0,0),(0,W),(L,0),(L,W)`,现在你需要从`x=0`出发，到`x=L`，不允许与障碍物接触,且车的所有部分都在`y=0`到`y=W`之间，不允许接触。
 ### 样例说明
 **样例 1:**
```
输入:
8 8
输出:
yes

解释:
给出`L=8`，`W=8`，障碍物坐标为`[[1,1],[6,6]]`。返回`yes`。
车的圆心可以从（0,5)到(2,5)到(5,2)到(8,2)，所以返回yes。
```

**样例 2:**
```
输入:
8 6
输出:
no

解释:
给出`L=8`，`W=6`，障碍物坐标为`[[1,1]]`,返回`no`。
不管如何驾驶，车总会与障碍物相切或者相交，这都是不被允许的。
```
 ### 参考代码
 这个题的思路是把 y=0 和 y=w 也看做障碍，然后如果两个障碍物之间无法通过车辆，则连一条线，相当于一个路障。然后如果说 y=0 和 y=w 最终通过路障连通起来了，说车无论如何也找不到一条路径可以穿过这条连起来的路障，否则就说明可以找到一个缺口从 x=0 开到 x=L

找连通性的问题，自然就是 BFS 最拿手的了。

```
[[python]]
OBSTACLE_MIN_DISTANCE = 6
BOUND_MIN_DISTANCE = 5

class Solution:
    """
    @param L: the length
    @param W: the width
    @param p:  the obstacle coordinates
    @return: yes or no
    """
    def drivingProblem(self, L, W, obstacles):
        from collections import deque
        
        # consider the upper & bottom line y=W, y=0, all obstacles
        # as nodes in a graph, if the car can not pass between two
        # nodes, we connect the two nodes with an edge in the graph.
        # the car can pass the road only if we CANNOT find a path
        # from start node y=W to the end node y=0
        
        queue = deque([(None, W)])
        visited = set([(None, W)])
        while queue:
            x, y = queue.popleft()
            # y <= 5 means (x, y) can connect the end node y=0
            if y <= BOUND_MIN_DISTANCE:
                return "no"
            for obstacle in obstacles:
                if (obstacle[0], obstacle[1]) in visited:
                    continue
                if not self.is_connected(x, y, obstacle[0], obstacle[1]):
                    continue
                queue.append((obstacle[0], obstacle[1]))
                visited.add((obstacle[0], obstacle[1]))
        return "yes"
    
    def is_connected(self, x1, y1, x2, y2):
        if x1 is None:
            return abs(y1 - y2) <= BOUND_MIN_DISTANCE
        # check the distance between (x1, y1) and (x2, y2) <= 6
        # 6 = 2 x (car radius + obstacle radius)
        return abs(x1 - x2) ** 2 + abs(y1 - y2) ** 2 <= OBSTACLE_MIN_DISTANCE ** 2  
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
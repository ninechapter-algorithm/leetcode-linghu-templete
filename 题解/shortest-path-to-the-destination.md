# 目的地的最短路径
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/shortest-path-to-the-destination/?utm_source=sc-github-wzz)
 ## 题目描述
 给定表示地图上坐标的2D数组，地图上只有值`0,1,2`.`0`表示可以通过，`1`表示不可通过，`2`表示目标位置。从坐标`[0,0]`开始，你只能上，下，左，右移动。找到可以到达目的地的最短路径，并返回路径的长度。
 ### 样例说明
 **样例1**

```plain
输入:
[
 [0, 0, 0],
 [0, 0, 1],
 [0, 0, 2]
]
输出: 4
说明: [0,0] -> [1,0] -> [2,0] -> [2,1] -> [2,2]
```

**样例2**

```plain
输入:
[
    [0,1],
    [0,1],
    [0,0],
    [0,2]
]
输出: 4
说明: [0,0] -> [1,0] -> [2,0] -> [3,0] -> [3,1]
```


 ### 参考代码
 使用双向宽度优先搜索的版本
```python
from collections import deque

DIRECTIONS = [
    (1, 0),
    (0, -1),
    (-1, 0),
    (0, 1),
]


class Solution:
    """
    @param targetMap: 
    @return: nothing
    """
    def shortestPath(self, targetMap):
        queue1 = deque([(0, 0)])
        target_x, target_y = self.find_target(targetMap)
        queue2 = deque([(target_x, target_y)])
        visited = {(0, 0): 1, (target_x, target_y): 2}
        
        distance = 0
        while queue1 or queue2:
            found = self.extend_to_next_level(targetMap, queue1, visited, 1)
            if found:
                return distance
            distance += 1
            found = self.extend_to_next_level(targetMap, queue2, visited, 2)
            if found:
                return distance
            distance += 1
        return -1
        
    def extend_to_next_level(self, targetMap, queue, visited, flag):
        for _ in range(len(queue)):
            x, y = queue.popleft()
            if visited.get((x, y)) == 3 - flag:
                return True
            for delta_x, delta_y in DIRECTIONS:
                _x = x + delta_x
                _y = y + delta_y
                if not self.is_valid(_x, _y, targetMap):
                    continue
                if visited.get((_x, _y)) == flag:
                    continue
                queue.append((_x, _y))
                visited[(_x, _y)] = flag
        return False
        
    def is_valid(self, x, y, targetMap):
        if not 0 <= x < len(targetMap) or not 0 <= y < len(targetMap[0]):
            return False
        return targetMap[x][y] != 1
        
    def find_target(self, targetMap):
        for i, row in enumerate(targetMap):
            for j, num in enumerate(row):
                if num == 2:
                    return i, j
        return -1, -1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
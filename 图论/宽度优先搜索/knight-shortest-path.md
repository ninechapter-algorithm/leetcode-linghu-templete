# 骑士的最短路线
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/knight-shortest-path/?utm_source=sc-github-wzz)
 ## 题目描述
 给定骑士在棋盘上的 `初始` 位置(一个2进制矩阵 `0` 表示空 `1` 表示有障碍物)，找到到达 `终点` 的最短路线，返回路线的长度。如果骑士不能到达则返回 `-1` 。
 ### 样例说明
 **例1:**
```
输入:
[[0,0,0],
 [0,0,0],
 [0,0,0]]
source = [2, 0] destination = [2, 2] 
输出: 2
解释:
[2,0]->[0,1]->[2,2]
```


**例2:**
```
输入:
[[0,1,0],
 [0,0,1],
 [0,0,0]]
source = [2, 0] destination = [2, 2] 
输出:-1
```

 ### 参考代码
 使用九章算法班中讲的 BFS。用 distance hash 来记录距离。
```
[[python]]
"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""

DIRECTIONS = [
    (-2, -1), (-2, 1), (-1, 2), (1, 2),
    (2, 1), (2, -1), (1, -2), (-1, -2),
]

class Solution:
        
    """
    @param grid: a chessboard included 0 (false) and 1 (true)
    @param source: a point
    @param destination: a point
    @return: the shortest path 
    """
    def shortestPath(self, grid, source, destination):
        queue = collections.deque([(source.x, source.y)])
        distance = {(source.x, source.y): 0}

        while queue:
            x, y = queue.popleft()
            if (x, y) == (destination.x, destination.y):
                return distance[(x, y)]
            for dx, dy in DIRECTIONS:
                next_x, next_y = x + dx, y + dy
                if (next_x, next_y) in distance:
                    continue
                if not self.is_valid(next_x, next_y, grid):
                    continue
                distance[(next_x, next_y)] = distance[(x, y)] + 1
                queue.append((next_x, next_y))
        return -1
        
    def is_valid(self, x, y, grid):
        n, m = len(grid), len(grid[0])

        if x < 0 or x >= n or y < 0 or y >= m:
            return False
            
        return not grid[x][y]
[[java]]
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */

public class Solution {
    public static final int[] dx = {1, 1, -1, -1, 2, 2, -2, -2};
    public static final int[] dy = {2, -2, 2, -2, 1, -1, 1, -1};
    /**
     * @param grid: a chessboard included 0 (false) and 1 (true)
     * @param source: a point
     * @param destination: a point
     * @return: the shortest path 
     */
    public int shortestPath(boolean[][] grid, Point source, Point destination) {
        if (grid == null || grid.length == 0
                || grid[0] == null || grid[0].length == 0) {
            return -1;
        }
        
        Queue<Point> queue = new ArrayDeque();
        Map<Integer, Integer> distance = new HashMap();
        
        int n = grid.length, m = grid[0].length;
        queue.offer(source);
        distance.put(source.x * m + source.y, 0);
        
        while (!queue.isEmpty()) {
            Point point = queue.poll();
            if (point.x == destination.x && point.y == destination.y) {
                return distance.get(point.x * m + point.y);
            }
            
            for (int i = 0; i < 8; i++) {
                int adjX = point.x + dx[i];
                int adjY = point.y + dy[i];
                if (!isValid(adjX, adjY, grid)) {
                    continue;
                }
                if (distance.containsKey(adjX * m + adjY)) {
                    continue;
                }
                
                distance.put(adjX * m + adjY, distance.get(point.x * m + point.y) + 1);
                queue.offer(new Point(adjX, adjY));
            }
        }
        
        return -1;
    }
    
    private boolean isValid(int x, int y, boolean[][] grid) {
        if (x < 0 || x >= grid.length || y < 0 || y >= grid[0].length) {
            return false;
        }
        return !grid[x][y];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
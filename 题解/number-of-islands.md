# 岛屿的个数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/number-of-islands/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个 01 矩阵，求不同的岛屿的个数。

0 代表海，1 代表岛，如果两个 1 相邻，那么这两个 1 属于同一个岛。我们只考虑上下左右为相邻。
 ### 样例说明
 
**样例 1：**
```
输入：
[
  [1,1,0,0,0],
  [0,1,0,0,1],
  [0,0,0,1,1],
  [0,0,0,0,0],
  [0,0,0,0,1]
]
输出：
3
```
**样例 2：**
```
输入：
[
  [1,1]
]
输出：
1
```
 ### 参考代码
 用九章算法班中讲到的 BFS 模板。
```
[[python]]
from collections import deque

DIRECTIONS = [(1, 0), (0, -1), (-1, 0), (0, 1)]

class Solution:
    """
    @param grid: a boolean 2D matrix
    @return: an integer
    """
    def numIslands(self, grid):
        if not grid or not grid[0]:
            return 0
            
        islands = 0
        visited = set()
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] and (i, j) not in visited:
                    self.bfs(grid, i, j, visited)
                    islands += 1
                    
        return islands                    
    
    def bfs(self, grid, x, y, visited):
        queue = deque([(x, y)])
        visited.add((x, y))
        while queue:
            x, y = queue.popleft()
            for delta_x, delta_y in DIRECTIONS:
                next_x = x + delta_x
                next_y = y + delta_y
                if not self.is_valid(grid, next_x, next_y, visited):
                    continue
                queue.append((next_x, next_y))
                visited.add((next_x, next_y))

    def is_valid(self, grid, x, y, visited):
        n, m = len(grid), len(grid[0])
        if not (0 <= x < n and 0 <= y < m):
            return False
        if (x, y) in visited:
            return False
        return grid[x][y]

# LeetCode 的用户请用下面的代码，因为 LeetCode 上的输入是 2D string array 而不是 boolean array
# from collections import deque

# class Solution:
#     """
#     @param grid: a boolean 2D matrix
#     @return: an integer
#     """
#     def numIslands(self, grid):
#         if not grid or not grid[0]:
#             return 0
        
#         islands = 0
#         for i in range(len(grid)):
#             for j in range(len(grid[0])):
#                 if grid[i][j] == '1':
#                     self.bfs(grid, i, j)
#                     islands += 1
                    
#         return islands                    
    
#     def bfs(self, grid, x, y):
#         queue = deque([(x, y)])
#         grid[x][y] = '0'
#         while queue:
#             x, y = queue.popleft()
#             for delta_x, delta_y in [(1, 0), (0, -1), (-1, 0), (0, 1)]:
#                 next_x = x + delta_x
#                 next_y = y + delta_y
#                 if not self.is_valid(grid, next_x, next_y):
#                     continue
#                 queue.append((next_x, next_y))
#                 grid[next_x][next_y] = '0'
                
#     def is_valid(self, grid, x, y):
#         n, m = len(grid), len(grid[0])
#         return 0 <= x < n and 0 <= y < m and grid[x][y] == '1'
[[java]]
class Coordinate {
    int x, y;
    public Coordinate(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

public class Solution {
    /**
     * @param grid a boolean 2D matrix
     * @return an integer
     */
    int[] deltaX = {0, 1, -1, 0};
    int[] deltaY = {1, 0, 0, -1};
    public int numIslands(boolean[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        if (grid[0] == null || grid[0].length == 0) {
            return 0;
        }
        
        int islands = 0;
        int n = grid.length, m = grid[0].length;
        boolean[][] visited = new boolean[n][m];
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] && !visited[i][j]) {
                    bfs(grid, i, j, visited);
                    islands++;
                }
            }
        }
        
        return islands;
    }
    
    private void bfs(boolean[][] grid, int x, int y, boolean[][] visited) {
        Queue<Coordinate> queue = new ArrayDeque<>();
        queue.offer(new Coordinate(x, y));
        visited[x][y] = true;
        
        while (!queue.isEmpty()) {
            Coordinate coor = queue.poll();
            for (int direction = 0; direction < 4; direction++) {
                int newX = coor.x + deltaX[direction];
                int newY = coor.y + deltaY[direction];
                if (!isVaild(grid, newX, newY, visited)) {
                    continue;
                }
                queue.offer(new Coordinate(newX, newY));
                visited[newX][newY] = true;
            }
        }
    }
    
    private boolean isVaild(boolean[][] grid, int x, int y, boolean[][] visited) {
        int n = grid.length, m = grid[0].length;
        if (x < 0 || x >= n || y < 0 || y >= m) {
            return false;
        }
        if (visited[x][y]) {
            return false;
        }
        return grid[x][y];
    }
}
```

也可以使用 DFS 的方法进行搜索。
DFS 分为两类：

1. 找所有路径的
2. 找所有节点的

第一类一般需要回溯，也就是把一个东西标记为使用过以后要把他标记回来。这样才能找到所有的路径。
第二类不需要回溯，因为只需要把所有连通的节点都标记一下即可。

DFS 来做这道题目虽然可以在 LintCode / LeetCode 等题库拿到 AC，但是在面试中并不推荐，因为 DFS 的深度可能会比较深，容易导致 StackOverflow。

```
[[python]]
class Solution:
    """
    @param grid: a boolean 2D matrix
    @return: an integer
    """
    def numIslands(self, grid):
        if not grid or not grid[0]:
            return 0
        
        n, m = len(grid), len(grid[0])
        visited = [[False] * m for _ in range(n)]
        
        islands = 0
        for row in range(n):
            for col in range(m):
                if self.is_island(grid, row, col, visited):
                    visited[row][col] = True
                    self.dfs(grid, row, col, visited)
                    islands += 1
                    
        return islands
        
    def is_island(self, grid, x, y, visited):
        n, m = len(grid), len(grid[0])
        if not (0 <= x < n and 0 <= y < m):
            return False
        if not grid[x][y]:
            return False
        return not visited[x][y]

    def dfs(self, grid, x, y, visited):
        dx = [1, 0, -1, 0]
        dy = [0, 1, 0, -1]
        for direction in range(4):
            newx = x + dx[direction]
            newy = y + dy[direction]
            
            if self.is_island(grid, newx, newy, visited):
                visited[newx][newy] = True
                self.dfs(grid, newx, newy, visited)
                # no backtracking
[[java]]
public class Solution {
    /**
     * @param grid: a boolean 2D matrix
     * @return: an integer
     */
    public int numIslands(boolean[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        if (grid[0] == null || grid[0].length == 0) {
            return 0;
        }
        
        int n = grid.length, m = grid[0].length;
        boolean[][] visited = new boolean[n][m];
        
        int islands = 0;
        for (int row = 0; row < n; row++) {
            for (int col = 0; col < m; col++) {
                if (isIsland(grid, row, col, visited)) {
                    visited[row][col] = true;
                    dfs(grid, row, col, visited);
                    islands++;
                }
            }
        }
        return islands;
    }
    
    private boolean isIsland(boolean[][] grid, int x, int y, boolean[][] visited) {
        int n = grid.length, m = grid[0].length;
        if (x < 0 || x >= n || y < 0 || y >= m) {
            return false;
        }
        if (!grid[x][y]) {
            return false;
        }
        return !visited[x][y];
    }
    
    private void dfs(boolean[][] grid, int x, int y, boolean[][] visited) {
        int[] dx = new int[]{1, 0, -1, 0};
        int[] dy = new int[]{0, 1, 0, -1};
        for (int direction = 0; direction < 4; direction++) {
            int newX = x + dx[direction];
            int newY = y + dy[direction];
            
            if (isIsland(grid, newX, newY, visited)) {
                visited[newX][newY] = true;
                dfs(grid, newX, newY, visited);
            }
        }
        // no backtracking
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
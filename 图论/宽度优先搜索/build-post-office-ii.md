# 邮局的建立 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/build-post-office-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个二维的网格，每一格可以代表墙 `2` ，房子 `1`，以及空 `0` (用数字0,1,2来表示)，在网格中找到一个位置去建立邮局，使得所有的房子到邮局的距离和是最小的。
返回所有房子到邮局的最小距离和，如果没有地方建立邮局，则返回`-1`.
 ### 样例说明
 **样例 1:**
```
输入：[[0,1,0,0,0],[1,0,0,2,1],[0,1,0,0,0]]
输出：8
解释： 在(1,1)处建立邮局，所有房子到邮局的距离和是最小的。
```

**样例 2:**
```
输入：[[0,1,0],[1,0,1],[0,1,0]]
输出：4
解释：在(1,1)处建立邮局，所有房子到邮局的距离和是最小的。
```
 ### 参考代码
 考点：
* bfs

题解：
* 本题采用bfs，首次遍历网格，对空地处进行bfs，搜索完成后如果存在房屋没有被vis标记则改空地不可以设置房屋。
* 朴素的bfs搜索过程中，sun+=dist;实现当前点距离和的更新。
* now.dis+1每次实现当前两点间距离的更新。
```java
class Coordinate {
    int x, y;
    public Coordinate(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

public class Solution {
    public int EMPTY = 0;
    public int HOUSE = 1;
    public int WALL = 2;
    public int[][] grid;
    public int n, m;
    public int[] deltaX = {0, 1, -1, 0};
    public int[] deltaY = {1, 0, 0, -1};
    
    private List<Coordinate> getCoordinates(int type) {
        List<Coordinate> coordinates = new ArrayList<>();
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] == type) {
                    coordinates.add(new Coordinate(i, j));
                }
            }
        }
        
        return coordinates;
    }
    
    private void setGrid(int[][] grid) {
        n = grid.length;
        m = grid[0].length;
        this.grid = grid;
    }
    
    private boolean inBound(Coordinate coor) {
        if (coor.x < 0 || coor.x >= n) {
            return false;
        }
        if (coor.y < 0 || coor.y >= m) {
            return false;
        }
        return grid[coor.x][coor.y] == EMPTY;
    }

    /**
     * @param grid a 2D grid
     * @return an integer
     */
    public int shortestDistance(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return -1;
        }
        
        // set n, m, grid
        setGrid(grid);
        
        List<Coordinate> houses = getCoordinates(HOUSE);
        int[][] distanceSum = new int[n][m];
        int[][] visitedTimes = new int[n][m];
        for (Coordinate house : houses) {
            bfs(house, distanceSum, visitedTimes);
        }
        
        int shortest = Integer.MAX_VALUE;
        List<Coordinate> empties = getCoordinates(EMPTY);
        for (Coordinate empty : empties) {
            if (visitedTimes[empty.x][empty.y] != houses.size()) {
                continue;
            }
            
            shortest = Math.min(shortest, distanceSum[empty.x][empty.y]);
        }
        
        if (shortest == Integer.MAX_VALUE) {
            return -1;
        }
        return shortest;
    }
    
    private void bfs(Coordinate start,
                     int[][] distanceSum,
                     int[][] visitedTimes) {
        Queue<Coordinate> queue = new LinkedList<>();
        boolean[][] hash = new boolean[n][m];
        
        queue.offer(start);
        hash[start.x][start.y] = true;
        
        int steps = 0;
        while (!queue.isEmpty()) {
            steps++;
            int size = queue.size();
            for (int temp = 0; temp < size; temp++) {
                Coordinate coor = queue.poll();
                for (int i = 0; i < 4; i++) {
                    Coordinate adj = new Coordinate(
                        coor.x + deltaX[i],
                        coor.y + deltaY[i]
                    );
                    if (!inBound(adj)) {
                        continue;
                    }
                    if (hash[adj.x][adj.y]) {
                        continue;
                    }
                    queue.offer(adj);
                    hash[adj.x][adj.y] = true;
                    distanceSum[adj.x][adj.y] += steps;
                    visitedTimes[adj.x][adj.y]++;
                } // direction
            } // for temp
        } // while
    }
}

//version 硅谷算法班
public class Solution {
    /**
     * @param grid: a 2D grid
     * @return: An integer
     */
    public int shortestDistance(int[][] grid) {
        // write your code here
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return -1;
        }

        int ans = Integer.MAX_VALUE;

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 0) {
                    ans = Math.min(ans, bfs(grid, i, j));
                }
            }
        }
        return ans == Integer.MAX_VALUE ? -1 : ans;
    }

    private int bfs(int[][] grid, int sx, int sy) {
        Queue<Integer> qx = new LinkedList<>();
        Queue<Integer> qy = new LinkedList<>();
        boolean[][] v = new boolean[grid.length][grid[0].length];

        qx.offer(sx);
        qy.offer(sy);
        v[sx][sy] = true;

        int[] dx = {1, -1, 0, 0};
        int[] dy = {0, 0, 1, -1};

        int dist = 0;
        int sum = 0;

        while (!qx.isEmpty()) {
            dist++;
            int size = qx.size();
            for (int i = 0; i < size; i++) {
                int cx = qx.poll();
                int cy = qy.poll();
                for (int k = 0; k < 4; k++) {
                    int nx = cx + dx[k];
                    int ny = cy + dy[k];
                    if (0 <= nx && nx < grid.length && 0 <= ny && ny < grid[0].length && !v[nx][ny]) {
                        v[nx][ny] = true;

                        if (grid[nx][ny] == 1) {
                            sum += dist;
                        }
                        if (grid[nx][ny] == 0) {
                            qx.offer(nx);
                            qy.offer(ny);
                        }
                    }
                }
            }
        }

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1 && !v[i][j]) {
                    return Integer.MAX_VALUE;
                }
            }
        }
        return sum;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
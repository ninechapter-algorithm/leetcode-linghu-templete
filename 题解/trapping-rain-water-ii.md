# 接雨水 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/trapping-rain-water-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给出 `n * m` 个非负整数，代表一张X轴上每个区域为 `1 * 1` 的 2d 海拔图, 计算这个海拔图最多能接住多少（面积）雨水。

![](https://lintcode-media.s3.amazonaws.com/problem/trapping-rain-water-ii.jpg "")
 ### 样例说明
 **样例 1:**
```
例如，给定一个 5*4 的矩阵： 
输入:
[[12,13,0,12],[13,4,13,12],[13,8,10,12],[12,13,12,12],[13,13,13,13]]
输出:
14
```

**样例 2:**
```
输入:
[[2,2,2,2],[2,2,3,4],[3,3,3,1],[2,3,4,5]]
输出:
0
```
 ### 参考代码
 将矩阵周边的格子都放到堆里，这些格子上面是无法盛水的。
每次在堆里挑出一个高度最小的格子 cell，把周围的格子加入到堆里。
这些格子被加入堆的时候，计算他们上面的盛水量。

```
盛水量 = cell.height - 这个格子的高度
```

当然如果这个值是负数，盛水量就等于 0。
```java
class Cell {
    public int x, y, height;
    Cell() {}
    Cell(int x, int y, int height) {
        this.x = x;
        this.y = y;
        this.height = height;
    }
}

class CellComparator implements Comparator<Cell> {
    @Override
    public int compare(Cell left, Cell right) {
        return left.height - right.height;
    }
}

public class Solution {
    int[] dx = {1, -1, 0, 0};
    int[] dy = {0, 0, 1, -1};
    
    public int trapRainWater(int[][] heights) {
        if (heights == null || heights.length == 0) {
            return 0;
        }
    
        PriorityQueue<Cell> minheap =  new PriorityQueue<>(new CellComparator());
        
        int n = heights.length;
        int m = heights[0].length;
        boolean[][] visited = new boolean[n][m];
        
        for (int i = 0; i < n; i++) {
            minheap.offer(new Cell(i, 0, heights[i][0]));
            minheap.offer(new Cell(i, m - 1, heights[i][m-1]));
            visited[i][0] = true;
            visited[i][m - 1] = true;
        }
        
        for (int i = 0; i < m; i++) {
            minheap.offer(new Cell(0, i, heights[0][i]));
            minheap.offer(new Cell(n-1, i, heights[n-1][i]));
            visited[0][i] = true;
            visited[n - 1][i] = true;
        }

        int water = 0;
        while (!minheap.isEmpty()) {
            Cell cell = minheap.poll();
            
            for (int i = 0; i < 4; i++) {
                int nx = cell.x + dx[i];
                int ny = cell.y + dy[i];
                
                if (nx < 0 || nx >= n || ny < 0 || ny >= m) {
                    continue;
                }
                if (visited[nx][ny]) {
                    continue;
                }
                
                visited[nx][ny] = true;
                minheap.offer(new Cell(nx, ny, Math.max(cell.height, heights[nx][ny])));
                water = water + Math.max(0, cell.height - heights[nx][ny]);
            }
        }
        
        return water;
    } 
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
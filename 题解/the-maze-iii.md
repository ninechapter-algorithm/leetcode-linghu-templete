# 迷宫III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/the-maze-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 在迷宫中有一个球，里面有空的空间和墙壁。球可以通过滚`up (u)`、`down (d)`、`left (l)`或右`right (r)`来穿过空的空间，`但它不会停止滚动直到撞到墙上`。当球停止时，它可以选择下一个方向。在这个迷宫里还有一个洞。如果球滚到洞里，球就会掉进洞里。
给定球的位置、洞的位置和迷宫，找出球如何通过移动`最短距离`落入洞内。距离是由球从起始位置(被排除)到洞(包括)所走过的空空间的数量来定义的。`用“u”、“d”、“l”和“r”来输出移动的方向`。由于可能有几种不同的最短路径，所以你应该输出字母顺序中（移动顺序中）最短的方法。如果球打不进洞，输出“impossible”。
迷宫由二维数组表示。1表示墙和0表示空的空间。你可以假设迷宫的边界都是墙。球和孔坐标用行和列的坐标表示。
 ### 样例说明
 **样例 1:**
```
输入:
[[0,0,0,0,0],[1,1,0,0,1],[0,0,0,0,0],[0,1,0,0,1],[0,1,0,0,0]]
[4,3]
[0,1]

输出:
"lul"
```
**样例 2:**
```
输入:
[[0,0,0,0,0],[1,1,0,0,1],[0,0,0,0,0],[0,1,0,0,1],[0,1,0,0,0]]
[0,0]
[1,1]
[2,2]
[3,3]
输出:
"impossible"
```

 ### 参考代码
 使用 BFS 算法。BFS 的每一步拓展一直走到撞墙为止。因为和最后要求的步数计算方法不同，所以一个点可能会被重复更新。
重复更新当且仅当发现一条更优路径，就重新放到队列里继续拓展。直到没有任何的节点能被更新，就退出。
```java
public class Solution {
    class Point {
        int x, y;
        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    
    class DistAndPath implements Comparable<DistAndPath> {
        int dist;
    	String path;
    	
    	public DistAndPath(int dist, String path) {
    		this.dist = dist;
    		this.path = path;
    	}
    	
    	public int compareTo(DistAndPath other) {
    	    if (this.dist != other.dist) {
    	        return this.dist - other.dist;
    	    }
    	    
    	    return path.compareTo(other.path);
    	}
    }
    
    public int[] dx = {0, 1, 0, -1};
    public int[] dy = {1, 0, -1, 0};
    public String[] directStr = {"r", "d", "l", "u"};

    /**
     * @param maze: the maze
     * @param ball: the ball position
     * @param hole: the hole position
     * @return: the lexicographically smallest way
     */
    public String findShortestWay(int[][] maze, int[] ball, int[] hole) {
        if (maze == null || maze.length == 0 || maze[0] == null || maze[0].length == 0) {
            return "impossible";
        }
        
        int n = maze.length;
        int m = maze[0].length;
        
        DistAndPath[][] cost = new DistAndPath[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                cost[i][j] = new DistAndPath(Integer.MAX_VALUE, "");
            }
        }
    
        cost[ball[0]][ball[1]].dist = 0;
 
        Queue<Point> queue = new LinkedList<>();
        queue.offer(new Point(ball[0], ball[1]));
        
        while (!queue.isEmpty()) {
            Point curt = queue.poll();
            for (int d = 0; d < 4; d++) {
                Point next = new Point(curt.x, curt.y);
                DistAndPath dp = new DistAndPath(cost[curt.x][curt.y].dist, cost[curt.x][curt.y].path + directStr[d]);
                while (!isWall(maze, next.x + dx[d], next.y + dy[d])) {
                    next.x += dx[d];
                    next.y += dy[d];
                    dp.dist += 1;
                    
                    if (next.x == hole[0] && next.y == hole[1]) {
                        break;
                    }
                }
                if (cost[next.x][next.y].compareTo(dp) > 0) {
                    cost[next.x][next.y] = dp;
                    if (next.x != hole[0] || next.y != hole[1]) {
                        queue.offer(next);
                    }
                }
            }
        }
        
        if (cost[hole[0]][hole[1]].dist == Integer.MAX_VALUE) {
            return "impossible";
        }
        
        return cost[hole[0]][hole[1]].path;
    }
    
    private boolean isWall(int[][] maze, int x, int y) {
        int n = maze.length;
        int m = maze[0].length;
        
        if (x < 0 || x >= n || y < 0 || y >= m) {
            return true;
        }
        
        return maze[x][y] == 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# Nearest Exit
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/nearest-exit/?utm_source=sc-github-wzz)
 ## 题目描述
 1789
 ### 样例说明
 1789
 ### 参考代码
 <p><br></p>
```java
// version: 高频题班
public class Solution {
    /**
     * @param rooms m x n 2D grid
     * @return nothing
     */
    static final int INF = 2147483647;
    int n, m;

    public void wallsAndGates(int[][] rooms) {
        // Write your code here
        n = rooms.length;
        if (n == 0) {
            return;
        }
        m = rooms[0].length;

        int dx[] = {0, 1, 0, -1};
        int dy[] = {1, 0, -1, 0};

        Queue<Integer> qx = new LinkedList<>();
        Queue<Integer> qy = new LinkedList<>();

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (rooms[i][j] == 0) {
                    qx.offer(i);
                    qy.offer(j);
                }
            }
        }

        while (!qx.isEmpty()) {
            int cx = qx.poll();
            int cy = qy.poll();

            for (int i = 0; i < 4; i++) {
                int nx = cx + dx[i];
                int ny = cy + dy[i];
                if (0 <= nx && nx < n && 0 <= ny && ny < m
                        && rooms[nx][ny] == INF) {
                    qx.offer(nx);
                    qy.offer(ny);
                    rooms[nx][ny] = rooms[cx][cy] + 1;
                }
            }
        }
    }

}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
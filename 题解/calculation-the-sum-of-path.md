# 路径数计算
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/calculation-the-sum-of-path/?utm_source=sc-github-wzz)
 ## 题目描述
 输入一个矩阵的长度为 `l`，宽度为 `w`，和三个必经点，问有多少种方法可以从左上角走到右下角（每一步，只能向右或者向下走），输入保证合法，有解。答案对 `1000000007` 取模。
 ### 样例说明
 
 ### 参考代码
 ```
[[python]]
MOD = 10 ** 9 + 7

"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""

class Solution:
    """
    @param l: The length of the matrix
    @param w: The width of the matrix
    @param points: three points 
    @return: The sum of the paths sum
    """
    def calculationTheSumOfPath(self, l, w, points):
        # preprocessing
        n, m, pairs = self.preprocessing(l, w, points)

        # state: dp[i][j] 代表从 0,0 走到 i,j 的方案总数
        dp = [[0] * m for _ in range(n)]
        
        # initialization: 第一行第一列方案数为1
        for i in range(n): 
            dp[i][0] = 1
        for i in range(m): 
            dp[0][i] = 1
        
        # function: dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        for i in range(1, n):
            for j in range(1, m):
                dp[i][j] = (dp[i - 1][j] + dp[i][j - 1]) % MOD
        
        # answer: sort points and multiply nubmer of paths together
        answer = 1
        for delta_x, delta_y in pairs:
            answer = (answer * dp[delta_x][delta_y]) % MOD
        return answer
        
    def preprocessing(self, l, w, original_points):
        points = [(p.x, p.y) for p in original_points]
        points.append((l, w))
        points.sort()
        
        prev_x, prev_y = 1, 1
        n, m = 0, 0
        pairs = []
        for x, y in points:
            pair = (x - prev_x, y - prev_y)
            pairs.append(pair)
            n = max(n, pair[0] + 1)
            m = max(m, pair[1] + 1)
            prev_x, prev_y = x, y
        
        return n, m, pairs
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

class ResultType {
    int n, m;
    List<Point> pairs;
    public ResultType(int n, int m, List<Point> pairs) {
        this.n = n;
        this.m = m;
        this.pairs = pairs;
    }
}

public class Solution {
    /**
     * @param l: The length of the matrix
     * @param w: The width of the matrix
     * @param points: three points 
     * @return: The sum of the paths sum
     */
    private int MOD = 1000000007;
    
    public long calculationTheSumOfPath(int l, int w, Point[] points) {
        // preprocessing
        ResultType result = preprocessing(l, w, points);
        int n = result.n, m = result.m;
        List<Point> pairs = result.pairs;
        
        // state: dp[i][j] 代表从 0,0 走到 i,j 的方案总数
        int[][] dp = new int[n][m];
        
        // initialization: 第一行第一列方案数为1
        for (int i = 0; i < n; i++) {
            dp[i][0] = 1;
        }
        for (int i = 0; i < m; i++) {
            dp[0][i] = 1;
        }
        
        // function: dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                dp[i][j] = (dp[i - 1][j] + dp[i][j - 1]) % MOD;
            }
        }
            
        // answer: sort points and multiply nubmer of paths together
        int answer = 1;
        for (Point delta: pairs) {
            answer = (int)((1L * answer * dp[delta.x][delta.y]) % MOD);
        }
        
        return answer;
    }
    
    private ResultType preprocessing(int l, int w, Point[] originalPoints) {
        List<Point> points = new ArrayList<>();
        for (int i = 0; i < originalPoints.length; i++) {
            points.add(new Point(originalPoints[i].x, originalPoints[i].y));
        }
        points.add(new Point(l, w));
        Collections.sort(points, new Comparator<Point>(){
            public int compare(Point p1, Point p2) {
                if (p1.x != p2.x) {
                    return p1.x - p2.x;
                }
                return p1.y - p2.y;
            }
        });
        
        int prevX = 1, prevY = 1;
        int n = 0, m = 0;
        List<Point> pairs = new ArrayList<>();
        for (Point p: points) {
            Point pair = new Point(p.x - prevX, p.y - prevY);
            pairs.add(pair);
            n = Math.max(n, pair.x + 1);
            m = Math.max(m, pair.y + 1);
            prevX = p.x;
            prevY = p.y;
        }
        
        return new ResultType(n, m, pairs);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
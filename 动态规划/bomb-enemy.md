# 炸弹袭击
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/bomb-enemy/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二维矩阵, 每一个格子可能是一堵墙 `W`,或者 一个敌人 `E` 或者空 `0` (数字 '0'), 返回你可以用一个炸弹杀死的最大敌人数. 炸弹会杀死所有在同一行和同一列没有墙阻隔的敌人。 由于墙比较坚固，所以墙不会被摧毁.
 ### 样例说明
 **样例1**

```
输入:
grid =[
     "0E00",
     "E0WE",
     "0E00"
]
输出: 3
解释:
把炸弹放在 (1,1) 能杀3个敌人
```

**样例2**

```
输入:
grid =[
     "0E00",
     "EEWE",
     "0E00"
]
输出: 2
解释:
P把炸弹放在 (0,0) 或 (0,3) 或 (2,0) 或 (2,3) 能杀2个敌人
```
 ### 参考代码
 预处理出每个点向四个方向能炸到的人数，然后枚举所有点，取最大值即可
```java
public class Solution {
    /**
     * @param grid Given a 2D grid, each cell is either 'W', 'E' or '0'
     * @return an integer, the maximum enemies you can kill using one bomb
     */
    public int maxKilledEnemies(char[][] grid) {
        // Write your code here
        int m = grid.length;
        int n = m > 0 ? grid[0].length : 0;

        int result = 0, rows = 0;
        int[] cols = new int[n];
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (j == 0 || grid[i][j-1] == 'W') {
                    rows = 0;
                    for (int k = j; k < n && grid[i][k] != 'W'; ++k)
                        if (grid[i][k] == 'E')
                            rows += 1;
                }
                if (i == 0 || grid[i-1][j] == 'W') {
                    cols[j] = 0;
                    for (int k = i; k < m && grid[k][j] != 'W'; ++k)
                        if (grid[k][j] == 'E')
                            cols[j] += 1;
                }

                if (grid[i][j] == '0' && rows + cols[j] > result)
                    result = rows + cols[j];
            }
        }
        return result;
    }
}

// 方法二
public class Solution {
    /**
     * @param grid Given a 2D grid, each cell is either 'W', 'E' or '0'
     * @return an integer, the maximum enemies you can kill using one bomb
     */
    public int maxKilledEnemies(char[][] A) {
        if (A == null || A.length == 0 || A[0].length == 0) {
            return 0;
        }
        
        int m = A.length;
        int n = A[0].length;
        int[][] up = new int[m][n];
        int[][] down = new int[m][n];
        int[][] left = new int[m][n];
        int[][] right = new int[m][n];
        int i, j, t;
        
        for (i = 0; i < m; ++i) {
            for (j = 0; j < n; ++j) {
                up[i][j] = 0;
                if (A[i][j] != 'W') {
                    if (A[i][j] == 'E') {
                        up[i][j] = 1;
                    }
                    
                    if (i - 1 >= 0) {
                        up[i][j] += up[i-1][j];
                    }
                }
            }
        }
        
        for (i = m - 1; i >= 0; --i) {
            for (j = 0; j < n; ++j) {
                down[i][j] = 0;
                if (A[i][j] != 'W') {
                    if (A[i][j] == 'E') {
                        down[i][j] = 1;
                    }
                    
                    if (i + 1 < m) {
                        down[i][j] += down[i+1][j];
                    }
                }
            }
        }
        
        for (i = 0; i < m; ++i) {
            for (j = 0; j < n; ++j) {
                left[i][j] = 0;
                if (A[i][j] != 'W') {
                    if (A[i][j] == 'E') {
                        left[i][j] = 1;
                    }
                    
                    if (j - 1 >= 0) {
                        left[i][j] += left[i][j-1];
                    }
                }
            }
        }
        
        for (i = 0; i < m; ++i) {
            for (j = n - 1; j >= 0; --j) {
                right[i][j] = 0;
                if (A[i][j] != 'W') {
                    if (A[i][j] == 'E') {
                        right[i][j] = 1;
                    }
                    
                    if (j + 1 < n) {
                        right[i][j] += right[i][j+1];
                    }
                }
            }
        }
        
        int res = 0;
        for (i = 0; i < m; ++i) {
            for (j = 0; j < n; ++j) {
                if (A[i][j] == '0') {
                    t = up[i][j] + down[i][j] + left[i][j] + right[i][j];
                    if (t > res) {
                        res = t;
                    }
                }
            }
        }
        
        return res;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
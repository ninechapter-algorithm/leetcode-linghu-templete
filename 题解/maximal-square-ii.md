# 最大矩阵II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximal-square-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个只有 `0` 和 `1` 组成的二维矩阵，找出最大的一个子矩阵，使得这个矩阵对角线上全是 `1` ，其他位置全是 `0` .
 ### 样例说明
 例1:
```
输入:
[[1,0,1,0,0],[1,0,0,1,0],[1,1,0,0,1],[1,0,0,1,0]]
输出:
9
解释:
[0,2]->[2,4]
```

例2:
```
输入:
[[1,0,1,0,1],[1,0,0,1,1],[1,1,1,1,1],[1,0,0,1,0]]
输出:
4
解释:
[0,2]->[1,3]
```


 ### 参考代码
 动态规划，u和l数组分别代表左边三角形的最大值和上方三角形的最大值，而f代表对角线到此点的最大长度。
直接三者求最小值转移即可。
```cpp
class Solution {
public:
    /**
     * @param matrix a matrix of 0 and 1
     * @return an integer
     */
    int maxSquare2(vector<vector<int>> &matrix) {
        // write your code here
        int n = matrix.size();
        if (n == 0)
            return 0;

        int m = matrix[0].size();
        if (m == 0)
            return 0;

        vector<vector<int>> f(n, vector<int>(m, 0));
        vector<vector<int>> u(n, vector<int>(m, 0));
        vector<vector<int>> l(n, vector<int>(m, 0));

        int length = 0;
        for (int i = 0; i < n; ++i)
            for (int j = 0; j < m; ++j) {
                if (matrix[i][j] == 0) {
                    f[i][j] = 0;
                    u[i][j] = l[i][j] = 1;
                    if (i > 0)
                        u[i][j] = u[i - 1][j] + 1;
                    if (j > 0)
                        l[i][j] = l[i][j - 1] + 1;
                } else {
                    u[i][j] = l[i][j] = 0;
                    if (i > 0 && j > 0)
                        f[i][j] = min(f[i - 1][j - 1], min(u[i - 1][j], l[i][j - 1])) + 1;
                    else 
                        f[i][j] = 1;
                }
                length = max(length, f[i][j]);
            }
        return length * length;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
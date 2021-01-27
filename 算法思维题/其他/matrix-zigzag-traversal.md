# 矩阵的之字型遍历
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/matrix-zigzag-traversal/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个包含 *m* x *n* 个元素的矩阵 (*m* 行, *n* 列), 求该矩阵的之字型遍历。
 ### 样例说明
 ```
样例 1:
	输入: [[1]]
	输出:  [1]

样例 2:
	输入:   
	[
    [1, 2,  3,  4],
    [5, 6,  7,  8],
    [9,10, 11, 12]
  ]

	输出:  [1, 2, 5, 9, 6, 3, 4, 7, 10, 11, 8, 12]


```

 ### 参考代码
 使用下标偏移变量来实现遍历。
遇到边界时改变偏移量。
直接模拟即可。
```java
public class Solution {
    /**
     * @param matrix: a matrix of integers
     * @return: an array of integers
     */ 
    public int[] printZMatrix(int[][] matrix) {
        // write your code here
        int x, y, dx, dy, count, m, n;
        x = y = 0;
        count = 1;
        dx = -1; dy = 1;
        m = matrix.length;
        n = matrix[0].length;
        int[] z = new int[m*n];
        z[0] = matrix[0][0];
        while (count<m*n) {
            if (x+dx>=0 && y+dy>=0 && x+dx<m && y+dy<n) {
                x += dx; y += dy;
            }
            else
                if (dx==-1 && dy ==1) {
                    if (y+1<n) ++y; else ++x;
                    dx = 1; dy = -1;
                }
                else {
                    if (x+1<m) ++x; else ++y;
                    dx = -1; dy = 1;
                }
            z[count] = matrix[x][y]; ++count;
        }
        return z;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 旋转图像
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rotate-image/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">给定一个N×N的二维矩阵表示图像，90度顺时针旋转图像。</span><br></p><p><br></p>
 ### 样例说明
 **样例1：**
```
输入:[[1,2],[3,4]]
输出:[[3,1],[4,2]]
```

**样例 2:**
```
输入:[[1,2,3],[4,5,6],[7,8,9]]
输出:[[7,4,1],[8,5,2],[9,6,3]]
```

 ### 参考代码
 You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Follow up:
Could you do this in-place?
```java
public class Solution {
    public void rotate(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }

        int length = matrix.length;

        for (int i = 0; i < length / 2; i++) {
            for (int j = 0; j < (length + 1) / 2; j++){
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[length - j - 1][i];
                matrix[length -j - 1][i] = matrix[length - i - 1][length - j - 1];
                matrix[length - i - 1][length - j - 1] = matrix[j][length - i - 1];
                matrix[j][length - i - 1] = tmp;
            }
        }   
    }
}


// version: 高频题班
//方法一
public class Solution {
    /**
     * @param matrix: A list of lists of integers
     * @return: Void
     */
    public void rotate(int[][] matrix) {
        // write your code here
        int n = matrix.length;
        for (int r = 0; r < (n + 1) / 2; r++) {
            for (int c = 0; c < n / 2; c++) {
                int tmp = matrix[r][c];
                matrix[r][c] = matrix[n - 1 - c][r];
                matrix[n - 1 - c][r] = matrix[n - 1 - r][n - 1 - c];
                matrix[n - 1 - r][n - 1 - c] = matrix[c][n - 1 - r];
                matrix[c][n - 1 - r] = tmp;
            }
        }
    }
}

//方法二：
public class Solution {
    /**
     * @param matrix: A list of lists of integers
     * @return: Void
     */
    public void rotate(int[][] matrix) {
        // write your code here
        int n = matrix.length;
        for (int r = 0; r < n / 2; r++) {
            for (int c = 0; c < n; c++) {
                int tmp = matrix[r][c];
                matrix[r][c] = matrix[n - r - 1][c];
                matrix[n - r - 1][c] = tmp;
            }
        }
        for (int r = 0; r < n; r++) {
            for (int c = r; c < n; c++) {
                int tmp = matrix[r][c];
                matrix[r][c] = matrix[c][r];
                matrix[c][r] = tmp;
            }
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
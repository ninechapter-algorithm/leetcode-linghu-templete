# 矩阵归零
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/set-matrix-zeroes/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个m×n矩阵，如果一个元素是0，则将其所在行和列全部元素变成0。

需要在原矩阵上完成操作。

 ### 样例说明
 **样例 1:**
```
输入:[[1,2],[0,3]]
输出:[[0,2],[0,0]]
```

**样例 2:**
```
输入:[[1,2,3],[4,0,6],[7,8,9]]
输出:[[1,0,3],[0,0,0],[7,0,9]]
```
 ### 参考代码
 Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

click to show follow up.

Follow up:
Did you use extra space?
A straight forward solution using O(mn) space is probably a bad idea.
A simple improvement uses O(m + n) space, but still not the best solution.
Could you devise a constant space solution?
```java
public class Solution {
     // using O(m+n) is easy, to enable O(1), we have to use the space within the matrix   
    public void setZeroes(int[][] matrix) {
        if(matrix == null || matrix.length == 0)
            return;
        
        int rows = matrix.length;
        int cols = matrix[0].length;
        
        boolean empty_row0 = false;
        boolean empty_col0 = false;
        for(int i = 0; i < cols; i++){
            if(matrix[0][i] == 0){
                empty_row0 = true;
                break;
            }
        }
        
        for(int i = 0; i < rows; i++){
            if(matrix[i][0] == 0){
                empty_col0 = true;
                break;
            }
        }
        
        for(int i = 1; i < rows; i++) {
            for(int j =1; j<cols; j++){
                if(matrix[i][j] == 0){
                    matrix[0][j] = 0;
                    matrix[i][0] = 0;
                }
            }
        }
        
        for(int i = 1; i<rows; i++) {
            for (int j=1; j< cols; j++) {
                if(matrix[0][j] == 0 || matrix[i][0] == 0)
                    matrix[i][j] = 0;
            }
        }
      
        if(empty_row0){
            for(int i = 0; i < cols; i++){
                matrix[0][i] = 0;
            }           
        }
        
        if(empty_col0){
            for(int i = 0; i < rows; i++){
                matrix[i][0] = 0;
            }           
        }

    }
}


```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 数独
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sudoku-solver/?utm_source=sc-github-wzz)
 ## 题目描述
 编写一个程序，通过填充空单元来解决数独难题。
空单元由数字`0`表示。
你可以认为只有一个唯一的解决方案。
 ### 样例说明
 **样例 1：**
```
给定的数独谜题:
```
![](http://lintcode-media.s3.amazonaws.com/problem/250px-Sudoku-by-L2G-20050714.svg.png)
```
返回结果：
```
![](http://lintcode-media.s3.amazonaws.com/problem/250px-Sudoku-by-L2G-20050714_solution.svg.png)
 ### 参考代码
 详细题解，请见九章微博：http://weibo.com/3948019741/BullK0fYo

采用递归+回溯模板来解决此问题：
1. 判定DFS的退出条件。

    (1) y越界，应该往下一行继续解。

  （2）x越界，代表数独解完，应该返回。

2. DFS的主体部分：

    把9个可能的值遍历一次，如果是OK的（使用独立 的Valid函数来判定行，列，BLOCK是否符合），继续DFS，否则回溯。

3. 最后的返回值：

    如果所有的可能性遍历都没有找到TRUE，最后应该返回FALSE，也就是当前情况无解。这个时候DFS会自动回溯到上一层再查找别的可能解。
```java
public class Solution {
    public void solveSudoku(char[][] board){
        solve(board);
    }

    public boolean solve(char[][] board) {
        for(int i = 0; i < 9; i++) {
            for(int j = 0; j < 9; j++){
                if(board[i][j] != '.'){
                    continue;
                }
                for(int k = 1; k <= 9; k++){
                    board[i][j] = (char) (k + '0');
                    if (isValid(board, i, j) && solve(board)){
                        return true;
                    }
                    board[i][j] = '.';
                }
                return false;
            }
        }
        return true;
    }
    
    
     public boolean isValid(char[][] board, int a, int b){
        Set<Character> contained = new HashSet<Character>();
        for(int j=0;j<9;j++){
            if(contained.contains(board[a][j])) return false;
            if(board[a][j]>'0' && board[a][j]<='9')
                contained.add(board[a][j]);
        }
            
        
    
        contained = new HashSet<Character>();
        for(int j=0;j<9;j++){
            if (contained.contains(board[j][b])) {
                return false;
            }
            if (board[j][b]>'0' && board[j][b]<='9') {
                contained.add(board[j][b]);
            }
        }
        
    
        contained = new HashSet<Character>();
        for (int m = 0; m < 3; m++) {
            for (int n = 0; n < 3; n++){
                int x = a / 3 * 3 + m, y = b / 3 * 3 + n;
                if (contained.contains(board[x][y])) {
                    return false;
                }
                if (board[x][y] > '0' && board[x][y] <= '9') {
                        contained.add(board[x][y]);
                }
            } 
        }
    
        return true;
    }
}

// 九章硅谷求职算法集训营版本
public class Solution {
    boolean[][] row = new boolean[9][9 + 1];
    boolean[][] col = new boolean[9][9 + 1];
    boolean[][][] block = new boolean[3][3][9 + 1];
    public void solveSudoku(int[][] board){
        int i, j, k;
        for (i = 0; i < 9; ++i) {
            for (j = 1; j <= 9; ++j) {
                row[i][j] = col[i][j] = false;
            }
        }

        for (i = 0; i < 3; ++i) {
            for (j = 0; j < 3; ++j) {
                for (k = 1; k <= 9; ++k) {
                    block[i][j][k] = false;
                }
            }
        }

        for (i = 0; i < 9; ++i) {
            for (j = 0; j < 9; ++j) {
                if (board[i][j] != 0) {
                    k = board[i][j];
                    row[i][k] = col[j][k] = true;
                    block[i / 3][j / 3][k] = true;
                }
            }
        }

        solve(board, 0, 0);
    }

    public boolean solve(int[][] board, int i, int j) {
        if (i == 9) {
            return true;
        }

        if (j == 9) {
            return solve(board, i + 1, 0);
        }

        if (board[i][j] != 0) {
            return solve(board, i, j + 1);
        }

        int k;
        for (k = 1; k <= 9; ++k) {
            if (!row[i][k] && !col[j][k] && !block[i/3][j/3][k]) {
                row[i][k] = col[j][k] = block[i/3][j/3][k] = true;
                board[i][j] = k;
                if (solve(board, i, j + 1)) {
                    return true;
                }
                
                board[i][j] = 0;
                row[i][k] = col[j][k] = block[i/3][j/3][k] = false;
            }
        }

        return false;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
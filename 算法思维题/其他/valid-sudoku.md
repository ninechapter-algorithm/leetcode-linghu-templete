# 判断数独是否合法
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/valid-sudoku/?utm_source=sc-github-wzz)
 ## 题目描述
 请判定一个数独是否有效。

该数独可能只填充了部分数字，其中缺少的数字用 `.` 表示。
 ### 样例说明
 **样例1:**

```plain
输入:
["53..7....","6..195...",".98....6.","8...6...3","4..8.3..1","7...2...6",".6....28.","...419..5","....8..79"]
输出: true
样例说明: 
这个数独如下图所示，他是合法的。
```

![Valid Sudoku](https://lintcode-media.s3.amazonaws.com/problem/valid-sudoku.png "Valid Sudoku")

**样例 2:**

```Input
输入:
["53..75...","6..195...",".98....6.","8...6...3","4..8.3..1","7...2...6",".6....28.","...419..5","....8..79"]
输出: false
样例说明: 
这个数独如下图所示。他是不合法的因为他的第一行和第六列有两个5。
```

![Invaild Sudoku](https://ws3.sinaimg.cn/large/6a8de5f4ly1g0s5st12otj206y06yaa5.jpg)
 ### 参考代码
 Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.


A partially filled sudoku which is valid.

Note:
A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.<div><br></div><div>详细题解请见九章微博：<a href="http://weibo.com/3948019741/BukaG6vKY" target="_blank">http://weibo.com/3948019741/BukaG6vKY</a></div>
```java
public class Solution {
    public boolean isValidSudoku(char[][] board) {
        boolean[] visited = new boolean[9];
        
        // row
        for(int i = 0; i<9; i++){
            Arrays.fill(visited, false);
            for(int j = 0; j<9; j++){
                if(!process(visited, board[i][j]))
                    return false;
            }
        }
        
        //col
        for(int i = 0; i<9; i++){
            Arrays.fill(visited, false);
            for(int j = 0; j<9; j++){
                if(!process(visited, board[j][i]))
                    return false;
            }
        }
        
        // sub matrix
        for(int i = 0; i<9; i+= 3){
            for(int j = 0; j<9; j+= 3){
                Arrays.fill(visited, false);
                for(int k = 0; k<9; k++){
                    if(!process(visited, board[i + k/3][ j + k%3]))
                    return false;                   
                }
            }
        }
        return true;
        
    }
    
    private boolean process(boolean[] visited, char digit){
        if(digit == '.'){
            return true;
        }
        
        int num = digit - '0';
        if ( num < 1 || num > 9 || visited[num-1]){
            return false;
        }
        
        visited[num-1] = true;
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
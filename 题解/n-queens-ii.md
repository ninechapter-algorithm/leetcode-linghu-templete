# N皇后问题 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/n-queens-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>根据n皇后问题，现在返回n皇后不同的解决方案的数量而不是具体的放置布局。</p>
 ### 样例说明
 例1:
```
输入: n=1
输出: 1
解释:
1:
1
```

例2:
```
输入: n=4
输出: 2
解释:
1:
0 0 1 0
1 0 0 0
0 0 0 1
0 1 0 0
2:
0 1 0 0 
0 0 0 1
1 0 0 0
0 0 1 0
```

 ### 参考代码
 dfs暴力搜索即可
```java
public class Solution {
    public static int sum;
    public int totalNQueens(int n) {
        sum = 0;
        int[] usedColumns = new int[n];
        placeQueen(usedColumns, 0);
        return sum;
    }
    public void placeQueen(int[] usedColumns, int row) {
        int n = usedColumns.length;
        
        if (row == n) {
            sum ++;
            return;
        }
        
        for (int i = 0; i < n; i++) {
            if (isValid(usedColumns, row, i)) {
                usedColumns[row] = i;
                placeQueen(usedColumns, row + 1);
            }
        }
    }
    public boolean isValid(int[] usedColumns, int row, int col) {
        for (int i = 0; i < row; i++) {
            if (usedColumns[i] == col) {
                return false;
            }
            if ((row - i) == Math.abs(col-usedColumns[i])) {
                return false;
            }
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
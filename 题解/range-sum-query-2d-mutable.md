# 范围矩阵元素和-可变的
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/range-sum-query-2d-mutable/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二维数组(矩阵), 需要查询它的某个子矩阵的元素的和, 同时矩阵内的元素可以被改变.

你需要实现三个方法:

- `NumMatrix(matrix)` 类的构造方法
- `sumRegion(row1, col1, row2, col2)` 返回处于 (row1, col1) 为左上角, (row2, col2) 为右下角的子矩阵内的元素的和
- `update(row, col, val)` 把 (row, col) 位置的元素更新为 `val`
 ### 样例说明
 **样例 1:**

```
输入:
  NumMatrix(
    [[3,0,1,4,2],
     [5,6,3,2,1],
     [1,2,0,1,5],
     [4,1,0,1,7],
     [1,0,3,0,5]]
  )
  sumRegion(2,1,4,3)
  update(3,2,2)
  sumRegion(2,1,4,3)
输出: 
  8
  10
```

**样例 2:**

```
输入: 
  NumMatrix([[1]])
  sumRegion(0, 0, 0, 0)
  update(0, 0, -1)
  sumRegion(0, 0, 0, 0)
输出: 
  1
  -1
```
 ### 参考代码
 Binary Indexed Tree - 2D 版本
```java
public class NumMatrix {
    private int[][] arr, bit;
    int n, m;
    
    /**
     * @return: nothing
     */
    public NumMatrix(int[][] matrix) {
        n = matrix.length;
        m = matrix[0].length;
        arr = new int[n][m];
        bit = new int[n + 1][m + 1];
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                update(i, j, matrix[i][j]);
            }
        }
    }
    
    public void update(int row, int col, int val) {
        int delta = val - arr[row][col];
        arr[row][col] = val;
        
        for (int i = row + 1; i <= n; i = i + lowbit(i)) {
            for (int j = col + 1; j <= m; j = j + lowbit(j)) {
                bit[i][j] += delta;
            }
        }
    }
    
    public int sumRegion(int row1, int col1, int row2, int col2) {
        return (
            prefixSum(row2, col2) -
            prefixSum(row2, col1 - 1) -
            prefixSum(row1 - 1, col2) +
            prefixSum(row1 - 1, col1 - 1)
        );
    }
    
    private int prefixSum(int row, int col) {
        int sum = 0;
        for (int i = row + 1; i > 0; i = i - lowbit(i)) {
            for (int j = col + 1; j > 0; j = j - lowbit(j)) {
                sum += bit[i][j];
            }
        }
        return sum;
    }
    
    private int lowbit(int x) {
        return x & (-x);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
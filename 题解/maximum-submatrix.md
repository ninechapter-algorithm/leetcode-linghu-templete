# 最大子矩阵
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-submatrix/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个大小为 `n x n` 的矩阵，里面元素为 `正整数` 和 `负整数` ，找到具有最大和的子矩阵。
 ### 样例说明
 **样例1**

```
输入:
matrix = [
    [1,3,-1],
    [2,3,-2],
    [-1,-2,-3]
]
输出: 9
解释:
具有最大和的子矩阵是:
[
    [1,3],
    [2,3]
]
```

**样例2**

```
输入:
matrix = [
    [1,1,1],
    [1,1,1],
    [1,1,1]
]
输出: 9
解释:
具有最大和的子矩阵是:
[
    [1,1,1],
    [1,1,1],
    [1,1,1]
]
```
 ### 参考代码
 枚举子矩阵的上下边界 up & down, 然后将这之间的数压缩为一个一维数组（降维攻击），剩下的任务就是一维数组如何求 Maximum Subarray 了。
```java
public class Solution {
  int n, m;
  
  /**
   * @param matrix: the given matrix
   * @return: the largest possible sum
   */
  public int maxSubmatrix(int[][] matrix) {
    if (matrix == null || matrix.length == 0) {
      return 0;
    }
    if (matrix[0] == null || matrix[0].length == 0) {
      return 0;
    }
    
    n = matrix.length;
    m = matrix[0].length;
    
    int[][] prefixColSum = getPrefixColSum(matrix);
    
    int max = Integer.MIN_VALUE;
    for (int up = 0; up < n; up++) {
      for (int down = up; down < n; down++) {
        int[] arr = compression(matrix, up, down, prefixColSum);
        max = Math.max(max, maximumSubarray(arr));
      }
    }
    
    return max;
  };
  
  private int maximumSubarray(int[] arr) {
    int min = 0, max = Integer.MIN_VALUE, sum = 0;
    
    for (int i = 0; i < m; i++) {
      sum += arr[i];
      max = Math.max(max, sum - min);
      min = Math.min(min, sum);
    }
    
    return max;
  }
  
  private int[] compression(int[][] matrix, int up, int down, int[][] prefixColSum) {
    int[] arr = new int[m];
    for (int i = 0; i < m; i++) {
      arr[i] = prefixColSum[down + 1][i] - prefixColSum[up][i];
    }
    
    return arr;
  }
  
  private int[][] getPrefixColSum(int[][] matrix) {
    int[][] sum = new int[n + 1][m];
    
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {
        sum[i + 1][j] = sum[i][j] + matrix[i][j];
      }
    }
    
    return sum;
  }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
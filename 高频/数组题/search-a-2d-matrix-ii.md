# 搜索二维矩阵 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/search-a-2d-matrix-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">写出一个高效的算法来搜索m×n矩阵中的值，返回这个值出现的次数。</span></p><p><span style="line-height: 1.42857143;">这个矩阵具有以下特性：</span><br></p><p><ul><li><span style="line-height: 1.42857143;">每行中的整数从左到右是排序的。</span><br></li><li><span style="line-height: 1.42857143;">每一列的整数从上到下是排序的。</span><br></li><li><span style="line-height: 1.42857143;">在每一行或每一列中没有重复的整数。</span></li></ul></p>
 ### 样例说明
 例1:
```
输入:
[[3,4]]
target=3
输出:1
```
例2:
```
输入:
    [
      [1, 3, 5, 7],
      [2, 4, 7, 8],
      [3, 5, 9, 10]
    ]
    target = 3
输出:2
```

 ### 参考代码
 从左下角开始，往右上角逼近
```python
class Solution:
    """
    @param matrix: An list of lists of integers
    @param target: An integer you want to search in matrix
    @return: An integer indicates the total occurrence of target in the given matrix
    """
    def searchMatrix(self, matrix, target):
        if matrix == [] or matrix[0] == []:
            return 0
            
        row, column = len(matrix), len(matrix[0])
        i, j = row - 1, 0
        count = 0
        while i >= 0 and j < column:
            if matrix[i][j] == target:
                count += 1
                i -= 1
                j += 1
            elif matrix[i][j] < target:
                j += 1
            elif matrix[i][j] > target:
                i -= 1
        return count
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
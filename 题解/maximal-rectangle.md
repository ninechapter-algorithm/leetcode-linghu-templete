# 最大矩形
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximal-rectangle/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个二维矩阵，权值为`False`和`True`，找到一个最大的矩形，使得里面的值全部为`True`，输出它的面积
 ### 样例说明
 **样例1**

```plain
输入:
[
  [1, 1, 0, 0, 1],
  [0, 1, 0, 0, 1],
  [0, 0, 1, 1, 1],
  [0, 0, 1, 1, 1],
  [0, 0, 0, 0, 1]
]
输出: 6
```

**样例2**

```plain
输入:
[
    [0,0],
    [0,0]
]
输出: 0
```


 ### 参考代码
 采用算法强化班中讲到的单调栈。
要做这个题之前先做直方图最大矩阵（Largest Rectangle in Histogram） 这个题。
这个题其实就是包了一层皮而已。一行一行的计算以当前行为矩阵的下边界时，最大矩阵是什么。
计算某一行为下边界时的情况，就可以转换为直方图最大矩阵问题了。
```python
class Solution:
    """
    @param matrix: a boolean 2D matrix
    @return: an integer
    """
    def maximalRectangle(self, matrix):
        if not matrix:
            return 0
            
        max_rectangle = 0
        heights = [0] * len(matrix[0])
        for row in matrix:
            for index, num in enumerate(row):
                heights[index] = heights[index] + 1 if num else 0
            max_rectangle = max(
                max_rectangle,
                self.find_max_rectangle(heights),
            )

        return max_rectangle

    def find_max_rectangle(self, heights):
        indices_stack = []
        max_rectangle = 0
        for index, height in enumerate(heights + [-1]):
            while indices_stack and heights[indices_stack[-1]] >= height:
                popped = indices_stack.pop(-1)
                left_bound = indices_stack[-1] if indices_stack else -1
                max_rectangle = max(
                    max_rectangle,
                    (index - left_bound - 1) * heights[popped],
                )
            indices_stack.append(index)
            print(indices_stack)
        
        return max_rectangle
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
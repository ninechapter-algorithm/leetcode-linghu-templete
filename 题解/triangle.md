# 数字三角形
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/triangle/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个数字三角形，找到从顶部到底部的最小路径和。每一步可以移动到下面一行的相邻数字上。

 ### 样例说明
 **样例 1**

```
输入下列数字三角形：
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
输出： 11
解释： 从顶到底部的最小路径和为11 ( 2 + 3 + 5 + 1 = 11)。
```

**样例 2**

```
输入下列数字三角形：
[
     [2],
    [3,2],
   [6,5,7],
  [4,4,8,1]
]
输出： 12
解释： 从顶到底部的最小路径和为12 ( 2 + 2 + 7 + 1 = 12)。
```


 ### 参考代码
 使用记忆化搜索的版本
时间复杂度 $O(n^2)$
空间复杂度 $O(n^2)$（额外耗费的空间）
```python
class Solution:
    """
    @param triangle: a list of lists of integers
    @return: An integer, minimum path sum
    """
    def minimumTotal(self, triangle):
        return self.divide_conquer(triangle, 0, 0, {})
        
    # 函数返回从 x, y 出发，走到最底层的最短路径值
    # memo 中 key 为二元组 (x, y)
    # memo 中 value 为从 x, y 走到最底层的最短路径值
    def divide_conquer(self, triangle, x, y, memo):
        if x == len(triangle):
            return 0
            
        # 如果找过了，就不要再找了，直接把之前找到的值返回
        if (x, y) in memo:
            return memo[(x, y)]

        left = self.divide_conquer(triangle, x + 1, y, memo)
        right = self.divide_conquer(triangle, x + 1, y + 1, memo)
        
        # 在 return 之前先把这次找到的最短路径值记录下来
        # 避免之后重复搜索
        memo[(x, y)] = min(left, right) + triangle[x][y]
        return memo[(x, y)]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
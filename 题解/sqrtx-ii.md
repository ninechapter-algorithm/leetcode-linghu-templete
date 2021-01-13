# 对x开根II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sqrtx-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 实现 `double sqrt(double x)` 并且 `x >= 0`。
计算并返回x开根后的值。
 ### 样例说明
 例1:
```
输入: n = 2 
输出: 1.41421356
```
例2:
```
输入: n = 3
输出: 1.73205081
```

 ### 参考代码
 ```python
class Solution:
    """
    @param: x: a double
    @return: the square root of x
    """
    def sqrt(self, x):
        if x >= 1:
            start, end = 1, x
        else:
            start, end = x, 1
        
        while end - start > 1e-10:
            mid = (start + end) / 2
            if mid * mid < x:
                start = mid
            else:
                end = mid
                
        return start
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
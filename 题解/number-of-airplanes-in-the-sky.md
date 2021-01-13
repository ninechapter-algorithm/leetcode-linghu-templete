# 数飞机
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/number-of-airplanes-in-the-sky/?utm_source=sc-github-wzz)
 ## 题目描述
 给出飞机的起飞和降落时间的列表，用序列 `interval` 表示. 请计算出天上同时最多有多少架飞机？
 ### 样例说明
 **样例 1:**

```
输入: [(1, 10), (2, 3), (5, 8), (4, 7)]
输出: 3
解释: 
第一架飞机在1时刻起飞, 10时刻降落.
第二架飞机在2时刻起飞, 3时刻降落.
第三架飞机在5时刻起飞, 8时刻降落.
第四架飞机在4时刻起飞, 7时刻降落.
在5时刻到6时刻之间, 天空中有三架飞机.
```

**样例 2:**

```
输入: [(1, 2), (2, 3), (3, 4)]
输出: 1
解释: 降落优先于起飞.
```
 ### 参考代码
 使用九章算法强化班中讲过的扫描线算法
```python
"""
Definition of Interval.
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    """
    @param airplanes: An interval array
    @return: Count of airplanes are in the sky.
    """
    def countOfAirplanes(self, airplanes):
        points = []
        for airplane in airplanes:
            points.append([airplane.start, 1])
            points.append([airplane.end, -1])
            
        number_of_airplane, max_number_of_airplane = 0, 0
        for _, count_delta in sorted(points):
            number_of_airplane += count_delta
            max_number_of_airplane = max(max_number_of_airplane, number_of_airplane)
            
        return max_number_of_airplane
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
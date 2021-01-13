# 会议室 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/meeting-rooms-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一系列的会议时间间隔intervals，包括起始和结束时间`[[s1,e1],[s2,e2],...] (si < ei)`，找到所需的最小的会议室数量。
 ### 样例说明
 **样例1**

```
输入: intervals = [(0,30),(5,10),(15,20)]
输出: 2
解释:
需要两个会议室
会议室1:(0,30)
会议室2:(5,10),(15,20)
```

**样例2**

```
输入: intervals = [(2,7)]
输出: 1
解释:
只需要1个会议室就够了
```
 ### 参考代码
 使用九章算法强化班中讲到的扫描线算法
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
    @param intervals: an array of meeting time intervals
    @return: the minimum number of conference rooms required
    """
    def minMeetingRooms(self, intervals):
        points = []
        for interval in intervals:
            points.append((interval.start, 1))
            points.append((interval.end, -1))
            
        meeting_rooms = 0
        ongoing_meetings = 0
        for _, delta in sorted(points):
            ongoing_meetings += delta
            meeting_rooms = max(meeting_rooms, ongoing_meetings)
            
        return meeting_rooms
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
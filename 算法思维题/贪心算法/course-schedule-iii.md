# 课程表 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/course-schedule-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 这里有 `n` 门不同的线上课程, 编号为 `1` 到 `n`. 每一节课都有持续时间(课程长度) `t` 和 在第 `d` 天关闭. 课程应连续持续 `t` 天，必须在第`d `天或之前完成, 你将从第一天开始.
给出 `n` 门线上课程用 `pairs (t, d)` 来表示, 你的任务是找到可以上的最大数量的课程数.
 ### 样例说明
 
 ### 参考代码
 贪心法 Greedy
课程按照 deadline 排序，从左到右扫描每个课程，依次学习。如果发现学了之后超过 deadline 的，就从之前学过的课程里扔掉一个耗时最长的。
因为这样可以使得其他的课程往前挪，而往前挪是没影响的。
所以挑最大值这个事情就是 Heap 的事情了
```python
import heapq


class Solution:
    """
    @param courses: duration and close day of each course
    @return: the maximal number of courses that can be taken
    """
    def scheduleCourse(self, courses):
        courses = sorted(courses, key=lambda x: x[1])
        curt_time = 0
        heap = []
        for duration, deadline in courses:
            curt_time += duration
            heapq.heappush(heap, -duration)
            if curt_time > deadline:
                curt_time -= (-heapq.heappop(heap))
                
        return len(heap)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
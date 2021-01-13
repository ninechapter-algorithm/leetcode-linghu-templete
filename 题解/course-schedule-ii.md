# 安排课程
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/course-schedule-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 你需要去上n门九章的课才能获得offer，这些课被标号为 `0` 到 `n-1` 。
有一些课程需要“前置课程”，比如如果你要上课程0，你需要先学课程1，我们用一个匹配来表示他们： `[0,1]`

给你课程的总数量和一些前置课程的需求，返回你为了学完所有课程所安排的学习顺序。

可能会有多个正确的顺序，你只要返回一种就可以了。如果不可能完成所有课程，返回一个空数组。
 ### 样例说明
 **例1:**
```
输入: n = 2, prerequisites = [[1,0]] 
输出: [0,1]
```
**例2:**
```
输入: n = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]] 
输出: [0,1,2,3] or [0,2,1,3]
```

 ### 参考代码
 拓扑排序，输出任意一种拓扑序列。
```python
class Solution:
    # @param {int} numCourses a total of n courses
    # @param {int[][]} prerequisites a list of prerequisite pairs
    # @return {int[]} the course order
    def findOrder(self, numCourses, prerequisites):
        # Write your code here
        edges = {i: [] for i in xrange(numCourses)}
        degrees = [0 for i in xrange(numCourses)] 
        for i, j in prerequisites:
            edges[j].append(i)
            degrees[i] += 1
        import Queue
        queue = Queue.Queue(maxsize = numCourses)
        
        for i in xrange(numCourses):
            if degrees[i] == 0:
                queue.put(i)

        order = []
        while not queue.empty():
            node = queue.get()
            order.append(node)

            for x in edges[node]:
                degrees[x] -= 1
                if degrees[x] == 0:
                    queue.put(x)

        if len(order) == numCourses:
            return order
        return []
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 寻找右区间
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-right-interval/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一组区间，对于每一个区间 i，检查是否存在一个区间 j，它的起始点大于或等于区间 i 的终点，这可以称为 j 在 i 的“右侧”。

对于任何区间，你需要存储的满足条件的区间 j 的最小索引，这意味着区间 j 有最小的起始点可以使其成为“右侧”区间。如果区间 j 不存在，则将区间 i 存储为 -1。最后，你需要输出一个值为存储的区间值的数组。
 ### 样例说明
 **样例 1:**
```
输入: intervals = [(1,2)]
输出: [-1]
解释:
集合中只有一个区间，所以输出-1。
```
**样例 2:**
```
输入: intervals = [(3,4),(2,3),(1,2)]
输出: [-1, 0, 1]
解释:
对于(3,4)，没有满足条件的“右侧”区间。
对于(2,3)，区间[3,4]具有最小的“右”起点;
对于(1,2)，区间[2,3]具有最小的“右”起点。
```
 ### 参考代码
 扫描线算法。
详见九章算法强化班
```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */

class Point {
    public int index, val;
    public boolean isStart;
    
    public Point(int index, int val, boolean isStart) {
        this.index = index;
        this.val = val;
        this.isStart = isStart;
    }
}

class Solution {
    private Comparator<Point> comparator = new Comparator<Point>() {
        public int compare(Point left, Point right) {
            if (left.val != right.val) {
                return left.val - right.val;
            }
            if (left.isStart) {
                return 1;
            }
            return -1;
        }
    };
    
    public int[] findRightInterval(Interval[] intervals) {
        List<Point> points = getSortedPoints(intervals);
        int[] rightArray = new int[intervals.length];
        Queue<Point> minheap = new PriorityQueue<>(comparator);
        
        // traverse points from right to left
        for (int i = points.size() - 1; i >= 0; i--) {
            Point point = points.get(i);
            if (point.isStart) {
                minheap.offer(point);
            } else {
                if (minheap.size() == 0) {
                    rightArray[point.index] = -1;
                } else {
                    rightArray[point.index] = minheap.peek().index;
                }
            }
        }
        
        return rightArray;
    }
    
    public List<Point> getSortedPoints(Interval[] intervals) {
        List<Point> points = new ArrayList<>(); 
        for (int i = 0; i < intervals.length; i++) {
            points.add(new Point(i, intervals[i].start, true));
            points.add(new Point(i, intervals[i].end, false));
        }
        Collections.sort(points, comparator);
        return points;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
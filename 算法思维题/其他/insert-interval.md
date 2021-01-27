# 插入区间
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/insert-interval/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一个<font color="#e76363"><b>无重叠的</b></font><span style="line-height: 1.42857143;">按照区间起始端点排序的区间列表。</span></p><p>在列表中插入一个新的区间，你要确保列表中的区间仍然有序且<font color="#e76363"><b>不重叠</b></font>（如果有必要的话，可以合并区间）。</p>
 ### 样例说明
 
**样例 1：**
```
输入:
(2, 5) into [(1,2), (5,9)]
输出:
[(1,9)]
```
**样例 2：**
```
输入:
(3, 4) into [(1,2), (5,9)]
输出:
[(1,2), (3,4), (5,9)]
```

 ### 参考代码
 定位到区间集与待插入的区间开始重合的部分，然后开始求交集。
交集一直延伸到相交区间的最末端。
```java
public class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        if (newInterval == null || intervals == null) {
            return intervals;
        }

        List<Interval> results = new ArrayList<Interval>();
        int insertPos = 0;

        for (Interval interval : intervals) {
            if (interval.end < newInterval.start) {
                results.add(interval);
                insertPos++;
            } else if (interval.start > newInterval.end) {
                results.add(interval);
            } else {
                newInterval.start = Math.min(interval.start, newInterval.start);
                newInterval.end = Math.max(interval.end, newInterval.end);
            }
        }

        results.add(insertPos, newInterval);

        return results;
    }
}

// version: 高频题班
public class Solution {
    /*
     * @param intervals: Sorted interval list.
     * @param newInterval: new interval.
     * @return: A new interval list.
     */
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        // write your code here
        List<Interval> ans = new ArrayList<>();

        int idx = 0;
        while (idx < intervals.size() && intervals.get(idx).start < newInterval.start) {
            idx++;
        }
        intervals.add(idx, newInterval);

        Interval last = null;
        for (Interval item : intervals) {
            if (last == null || last.end < item.start) {
                ans.add(item);
                last = item;
            } else {
                last.end = Math.max(last.end, item.end); // Modify the element already in list
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 合并K个排序间隔列表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/merge-k-sorted-interval-lists/?utm_source=sc-github-wzz)
 ## 题目描述
 将K个排序的间隔列表合并到一个排序的间隔列表中，你需要合并重叠的间隔。
 ### 样例说明
 **样例1**

```
输入: [
  [(1,3),(4,7),(6,8)],
  [(1,2),(9,10)]
]
输出: [(1,3),(4,8),(9,10)]
```

**样例2**

```
输入: [
  [(1,2),(5,6)],
  [(3,4),(7,8)]
]
输出: [(1,2),(3,4),(5,6),(7,8)]
```
 ### 参考代码
 使用 PriorityQueue 的版本
假设总共有 N 个整数，一共 K 个数组
时间复杂度 $O(NlogK)$
空间复杂度 $O(K)$
```java
class Pair {
    int row, col;
    public Pair(int row, int col) {
        this.row = row;
        this.col = col;
    }
}

public class Solution {
    /**
     * @param intervals: the given k sorted interval lists
     * @return:  the new sorted interval list
     */
    public List<Interval> mergeKSortedIntervalLists(List<List<Interval>> intervals) {
        int k = intervals.size();
        PriorityQueue<Pair> queue = new PriorityQueue<>(
          k,
          new Comparator<Pair>() {
            public int compare(Pair e1, Pair e2) {
                return intervals.get(e1.row).get(e1.col).start - 
                  intervals.get(e2.row).get(e2.col).start;
            }
          }
        );
        
        for (int i = 0; i < intervals.size(); i ++) {
            if (intervals.get(i).size() > 0) {
                queue.add(new Pair(i, 0));
            }
        }
        
        List<Interval> result = new ArrayList<>();
        while (!queue.isEmpty()) {
            Pair pair = queue.poll();
            result.add(intervals.get(pair.row).get(pair.col));
            pair.col++;
            if (pair.col < intervals.get(pair.row).size()) {
                queue.add(pair);
            }
        }
        
        return merge(result);
    }
    
    private List<Interval> merge(List<Interval> intervals) {
        if (intervals.size() <= 1) {
            return intervals;
        }
        
        List<Interval> result = new ArrayList<>();
        int start = intervals.get(0).start;
        int end = intervals.get(0).end;
        for (Interval interval : intervals) {
            if (interval.start <= end) {
                end = Math.max(end, interval.end);
            } else {
                result.add(new Interval(start, end));
                start = interval.start;
                end = interval.end;
            }
        }
        // kickoff the last interval
        result.add(new Interval(start, end));
        
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
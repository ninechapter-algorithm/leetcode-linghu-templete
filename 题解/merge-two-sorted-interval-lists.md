# 合并两个排序的间隔列表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/merge-two-sorted-interval-lists/?utm_source=sc-github-wzz)
 ## 题目描述
 合并两个已排序的区间列表，并将其作为一个新的有序区间列表返回。新的区间列表应该通过拼接两个列表的区间并按升序排序。
 ### 样例说明
 **样例1**

```
输入: [(1,2),(3,4)] and list2 = [(2,3),(5,6)]
输出: [(1,4),(5,6)]
解释:
(1,2),(2,3),(3,4) --> (1,4)
(5,6) --> (5,6)
```



**样例2**

```
输入: [(1,2),(3,4)] 和 list2 = [(4,5),(6,7)]
输出: [(1,2),(3,5),(6,7)]
解释:
(1,2) --> (1,2)
(3,4),(4,5) --> (3,5)
(6,7) --> (6,7)
```
 ### 参考代码
 正如课上说的，用一个 last 来记录最后一个还没有被放到 merge results 里的 Interval，用于和新加入的 interval 比较看看能不能合并到一起。

时间复杂度 $O(n + m)$
```java
public class Solution {
    /**
     * @param list1: one of the given list
     * @param list2: another list
     * @return: the new sorted list of interval
     */
    public List<Interval> mergeTwoInterval(List<Interval> list1, List<Interval> list2) {
        List<Interval> results = new ArrayList<>();
        if (list1 == null || list2 == null) {
            return results;
        }
        
        Interval last = null, curt = null;
        int i = 0, j = 0;
        while (i < list1.size() && j < list2.size()) {
            if (list1.get(i).start < list2.get(j).start) {
                curt = list1.get(i);
                i++;
            } else {
                curt = list2.get(j);
                j++;
            }
            
            last = merge(results, last, curt);
        }
        
        while (i < list1.size()) {
            last = merge(results, last, list1.get(i));
            i++;
        }
        
        while (j < list2.size()) {
            last = merge(results, last, list2.get(j));
            j++;
        }
        
        if (last != null) {
        	results.add(last);
        }
        return results;
    }
    
    private Interval merge(List<Interval> results, Interval last, Interval curt) {
        if (last == null) {
            return curt;
        }
        
        if (curt.start > last.end) {
            results.add(last);
            return curt;
        }
        
        last.end = Math.max(last.end, curt.end);
        return last;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
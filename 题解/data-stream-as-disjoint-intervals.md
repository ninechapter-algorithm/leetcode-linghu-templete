# 将数据流变为多个不相交区间
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/data-stream-as-disjoint-intervals/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个非负整数的数据流输入 a1，a2，…，an，…，将到目前为止看到的数字总结为不相交的区间列表。

例如，假设数据流中的整数为 1，3，7，2，6，…，每次的总结为：
```
[1, 1]
[1, 1], [3, 3]
[1, 1], [3, 3], [7, 7]
[1, 3], [7, 7]
[1, 3], [6, 7]
```
 ### 样例说明
 **Example 1:**
```
输入：["SummaryRanges","addNum","getIntervals","addNum","getIntervals","addNum","getIntervals","addNum","getIntervals","addNum","getIntervals"],[[],[1],[],[3],[],[7],[],[2],[],[6],[]]
输出：[null,null,[[1,1]],null,[[1,1],[3,3]],null,[[1,1],[3,3],[7,7]],null,[[1,3],[7,7]],null,[[1,3],[6,7]]]
解释：add(1)->get([[1, 1]])->add(3)->get([[1, 1], [3, 3]])->add(7)->get([[1, 1], [3, 3], [7, 7]])->add(2)-merge(1,2,3)->get([[1, 3], [7, 7]])->add(6)->merge(6,7)->get([[1, 3], [6, 7]])
```


**Example 2:**
```
输入：["SummaryRanges","addNum","getIntervals","addNum","getIntervals"],[[],[4],[],[3],[]]
输出：[null,null,[4,4],null,[3,4]]
解释：add(4)->get([[4, 4]])->add(3)->merge(3,4)->get([[3, 4]])
```
 ### 参考代码
 无脑使用并查集的做法。
相对于使用红黑树的做法而言，addNum 的操作变快了，O(1)。但是 getIntervals 因为需要排序，所以变慢了，O(NlogN)
红黑树是 addNum O(logN)，getIntervals O(N)

不能说哪个一个最好。因为取决于 addNum 和 getIntervals 的调用频率。
```python
class SummaryRanges:
    
    def __init__(self):
        self.father = dict()
        self.val2interval = dict()

    def addNum(self, val):
        if val in self.father:
            return
        
        self.father[val] = val
        self.val2interval[val] = [val, val]
        if val - 1 in self.father:
            self.merge(val - 1, val)
            
        if val + 1 in self.father:
            self.merge(val + 1, val)
      
    def getIntervals(self):
        return [
            self.val2interval[val]
            for val in sorted(self.father.keys())
            if self.father[val] == val
        ]
        
    def merge(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)
        self.father[root_a] = root_b
        self.val2interval[root_b] = [
            min(self.val2interval[root_a][0], self.val2interval[root_b][0]),
            max(self.val2interval[root_a][1], self.val2interval[root_b][1]),
        ]
    
    def find(self, a):
        if a == self.father[a]:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
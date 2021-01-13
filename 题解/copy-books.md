# 书籍复印
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/copy-books/?utm_source=sc-github-wzz)
 ## 题目描述
 给定 `n` 本书, 第 `i` 本书的页数为 `pages[i]`. 现在有 `k` 个人来复印这些书籍, 而每个人只能复印编号连续的一段的书, 比如一个人可以复印 `pages[0], pages[1], pages[2]`, 但是不可以只复印 `pages[0], pages[2], pages[3]` 而不复印 `pages[1]`.

所有人复印的速度是一样的, 复印一页需要花费一分钟, 并且所有人同时开始复印. 怎样分配这 `k` 个人的任务, 使得这 `n` 本书能够被尽快复印完?

返回完成复印任务最少需要的分钟数.
 ### 样例说明
 **样例 1:**

```
输入: pages = [3, 2, 4], k = 2
输出: 5
解释: 第一个人复印前两本书, 耗时 5 分钟. 第二个人复印第三本书, 耗时 4 分钟.
```

**样例 2:**

```
输入: pages = [3, 2, 4], k = 3
输出: 4
解释: 三个人各复印一本书.
```
 ### 参考代码
 使用九章算法强化班中讲过的基于答案值域的二分法。
答案的范围在 max(pages)~sum(pages) 之间，每次二分到一个时间 time_limit 的时候，用贪心法从左到右扫描一下 pages，看看需要多少个人来完成抄袭。
如果这个值 <= k，那么意味着大家花的时间可能可以再少一些，如果 > k 则意味着人数不够，需要降低工作量。

时间复杂度 $O(nlog(sum))$ 是该问题时间复杂度上的最优解法
```python
class Solution:
    """
    @param pages: an array of integers
    @param k: An integer
    @return: an integer
    """
    def copyBooks(self, pages, k):
        if not pages:
            return 0
            
        start, end = max(pages), sum(pages)
        while start + 1 < end:
            mid = (start + end) // 2
            if self.get_least_people(pages, mid) <= k:
                end = mid
            else:
                start = mid
                
        if self.get_least_people(pages, start) <= k:
            return start
            
        return end
        
    def get_least_people(self, pages, time_limit):
        count = 0
        time_cost = 0 
        for page in pages:
            if time_cost + page > time_limit:
                count += 1
                time_cost = 0
            time_cost += page
            
        return count + 1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
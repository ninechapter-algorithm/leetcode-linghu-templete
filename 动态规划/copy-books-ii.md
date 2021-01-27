# 书籍复印 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/copy-books-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定 `n` 本书, 每本书具有相同的页数. 现在有 `k` 个人来复印这些书. 其中第 `i` 个人需要 `times[i]` 分钟来复印一本书. 每个人可以复印任意数量的书. 怎样分配这 `k` 个人的任务, 使得这 `n` 本书能够被尽快复印完?

返回完成复印任务最少需要的分钟数.
 ### 样例说明
 **样例 1:**

```
输入: n = 4, times = [3, 2, 4]
输出: 4
解释: 第一个人复印 1 本书, 花费 3 分钟. 第二个人复印 2 本书, 花费 4 分钟. 第三个人复印 1 本书, 花费 4 分钟.
```

**样例 2:**

```
输入: n = 4, times = [3, 2, 4, 5]
输出: 4
解释: 使用与样例 1相同的策略, 第四个人不参与复印.
```
 ### 参考代码
 可以使用二分或者动态规划解决这道题目. 不过更推荐二分答案的写法, 它更节省空间, 思路简洁, 容易编码.

对于假定的时间上限 `tm` 我们可以使用贪心的思想判断这 `k` 个人能否完成复印 `n` 本书的任务: 每个人都在规定时间内尽可能多地复印, 判断他们复印的总数是否不小于 `n` 即可.

而时间上限 `tm` 与可否完成任务(0或1)这两个量之间具有单调性关系, 所以可以对 `tm` 进行二分查找, 查找最小的 `tm`, 使得任务可以完成.
```python
class Solution:
    """
    @param n: An integer
    @param times: an array of integers
    @return: an integer
    """
    def copyBooksII(self, n, times):
        l = 1 
        r = min(times) * n 
        while l < r:
            mid = (l + r) // 2
            if self.ok(n, times, mid):
                r = mid 
            else:
                l = mid + 1 
        return l 
    
    def ok(self, n, times, tm):
        num = 0
        for i in times:
            num += tm // i
        return n <= num

class Solution:
    # @param n: an integer
    # @param times: a list of integers
    # @return: an integer
    def copyBooksII(self, n, times):
        # write your code here
        k = len(times)
        ans = 0
        eachTime = []
        totalTime = []
        for i in range(k):
            self.heapAdd(eachTime, totalTime, times[i], 0)
        for i in range(n):
            ans = totalTime[0]
            x = eachTime[0]
            self.heapDelete(eachTime, totalTime)
            self.heapAdd(eachTime, totalTime, x, ans+x)
        ans = 0
        for i in range(len(totalTime)):
            ans = max(ans, totalTime[i])
        return ans

    def heapAdd(self, eachTime, totalTime, et, tt):
        eachTime.append(et)
        totalTime.append(tt)
        n = len(eachTime)-1
        while n > 0 and eachTime[n]+totalTime[n] < eachTime[(n-1)//2]+totalTime[(n-1)//2]:
            eachTime[n], eachTime[(n-1)//2] = eachTime[(n-1)//2], eachTime[n]
            totalTime[n], totalTime[(
                n-1)//2] = totalTime[(n-1)//2], totalTime[n]
            n = (n-1)//2

    def heapDelete(self, eachTime, totalTime):
        n = len(eachTime)-1
        if n >= 0:
            eachTime[0] = eachTime[n]
        if n >= 0:
            totalTime[0] = totalTime[n]
        if len(eachTime) > 0:
            eachTime.pop()
        if len(totalTime) > 0:
            totalTime.pop()
        n = 0
        while n*2+1 < len(eachTime):
            t = n*2+1
            if t+1 < len(eachTime) and eachTime[t+1]+totalTime[t+1] < eachTime[t]+totalTime[t]:
                t += 1
            if eachTime[n]+totalTime[n] <= eachTime[t]+totalTime[t]:
                break
            eachTime[n], eachTime[t] = eachTime[t], eachTime[n]
            totalTime[n], totalTime[t] = totalTime[t], totalTime[n]
            n = t
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
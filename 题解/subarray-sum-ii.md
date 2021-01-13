# 子数组求和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/subarray-sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个正整数数组 `A` 和一个区间. 返回和在给定区间范围内的子数组数量.
 ### 样例说明
 **样例 1:**

```
输入: A = [1, 2, 3, 4], start = 1, end = 3
输出: 4
解释: 所有可能的子数组: [1](和为1), [1, 2](和为3), [2](和为2), [3](和为3).
```

**样例 2:**

```
输入: A = [1, 2, 3, 4], start = 1, end = 100
输出: 10
解释: 任意子数组都可以.
```
 ### 参考代码
 **O(N) 的两根指针的算法**

其实需要三根指针, 因为需要额外记录一下从哪个位置开始的加和已经 >= start 了.

对于每一个左端点 left, 求出对应的两个右端点 right_start, right_end. 前者表示最左边的使得 [left, right_start] 子数组的和不小于 start 的点, 而后者表示最右边的使得 [left, right_end] 子数组的和不大于 end 的点.

right_end - right_start + 1 就是以 left 为左端点的合法子数组的数量.

从左到右枚举 left, 而 right_start, right_end 随着left的增长也是只增不减的, 所以时间复杂度是 O(N)

**O(NlogN) 的二分法**

求出一个前缀和数组, 然后对于每一个前缀和 presum[right], 我们要求出两个点 left_start, left_end. 前者表示最左边的使得 [left_start, right] 子数组和不大于 end 的点, 后者表示最右边的使得 [left_end, right] 子数组和不小于 start 的点.

枚举 right, 我们可以在 presum[0..right] 上二分查找确定 left_start, left_end.

**总结**

上面两种方法是相通的, 都是对于子数组的一个端点, 确认另外一个端点的范围. 在枚举其中一个端点的过程, 另外一个端点的范围是单调的, 所以可以使用两根指针 O(N) 地完成.

可以把两根指针和二分法综合一下, 不过这样理论时间复杂度是不变的, 没有很大的必要. 以上两种方法推荐第一种, 复杂度更低.
```python
class Solution:
    """
    @param A: An integer array
    @param start: An integer
    @param end: An integer
    @return: the number of possible answer
    """
    def subarraySumII(self, A, start, end):
        n = len(A)
        big_sum, small_sum = 0, 0
        big_end, small_end = 0, 0
        ans = 0
        for i in range(n):
            small_end = max(small_end, i)
            big_end = max(big_end, i)
            while small_end < n and small_sum + A[small_end] < start:
                small_sum += A[small_end]
                small_end += 1
            while big_end < n and big_sum + A[big_end] <= end:
                big_sum += A[big_end]
                big_end += 1
            
            if big_end - small_end > 0:
                ans += big_end - small_end
                
            if small_end > i:
                small_sum -= A[i]
            
            if big_end > i:
                big_sum -= A[i]
            
        return ans
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
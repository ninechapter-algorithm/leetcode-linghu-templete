# 数组划分II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/partition-array-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 将一个没有经过排序的整数数组划分为 3 部分:
1.第一部分中所有的值都 < low
2.第二部分中所有的值都 >= low并且 <= high
3.第三部分中所有的值都 > high
返回任意一种可能的情况。
 ### 样例说明
 例1:
```
输入:
[4,3,4,1,2,3,1,2]
2
3
输出:
[1,1,2,3,2,3,4,4]
解释:
[1,1,2,2,3,3,4,4] 也对, 但 [1,2,1,2,3,3,4,4] 不对
```

例2:
```
输入:
[3,2,1]
2
3
输出:
[1,2,3]
```


 ### 参考代码
 类似快速排序的思路去分割即可，遇到不满足即交换。
```python
# 参考程序1
class Solution:
    # @param {int[]} nums an integer array
    # @param {int} low an integer
    # @param {int} high an integer
    # @return {int[]} any of the possible solutions
    def partition2(self, nums, low, high):
        # Write your code here
        if len(nums) <= 1:
            return
        
        pl, pr = 0, len(nums) - 1
        i = 0
        while i <= pr:
            if nums[i] < low:
                nums[pl], nums[i] = nums[i], nums[pl]
                pl += 1
                i += 1
            elif nums[i] > high:
                nums[pr], nums[i] = nums[i], nums[pr]
                pr -= 1
            else:
                i += 1

# 参考程序2
class Solution:
    # @param {int[]} nums an integer array
    # @param {int} low an integer
    # @param {int} high an integer
    # @return nothing
    def partition2(self, nums, low, high):
        # Write your code here
        left = 0
        right = len(nums) - 1

        # 首先把区间分为 < low 和 >= low 的两个部分 
        while left <= right:
            while left <= right and nums[left] < low:
                left = left + 1
            while left <= right and nums[right] >= low:
                right = right - 1
            if left <= right:
                nums[right],nums[left] = nums[left],nums[right]
                left = left + 1
                right = right - 1

        right = len(nums) - 1
        # 然后从 >= low 的部分里分出 <= high 和 > high 的两个部分
        while left <= right:
            while left <= right and nums[left] <= high:
                left = left + 1
            while left <= right and nums[right] > high:
                right = right - 1
            if left <= right:
                nums[right],nums[left] = nums[left],nums[right]
                left = left + 1
                right = right - 1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
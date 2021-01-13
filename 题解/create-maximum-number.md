# 创建最大数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/create-maximum-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给出两个长度分别是`m`和`n`的数组来表示两个大整数，数组的每个元素都是数字`0-9`。从这两个数组当中选出`k`个数字来创建一个最大数，其中`k`满足`k <= m + n`。选出来的数字在创建的最大数里面的位置必须和在原数组内的相对位置一致。返回`k`个数的数组。你应该尽可能的去优化算法的时间复杂度和空间复杂度。
 ### 样例说明
 **样例 1:**
```
输入：nums1 = [3, 4, 6, 5]， nums2 = [9, 1, 2, 5, 8, 3]，k = 5
输出：[9, 8, 6, 5, 3]
解释：
从第一个数组选择[6, 5]，从第二个数组选择[9, 8, 3]
```
**样例 2:**
```
输入：nums1 = [6, 7]， nums2 = [6, 0, 4]，k = 5
输出：[6, 7, 6, 0, 4]
解释：
从第一个数组选择[6, 7]，从第二个数组选择[6, 0, 4]
```

**样例 3:**
```
输入：nums1 = [3, 9]， nums2 = [8, 9]，k = 3
输出：[9, 8, 9]
解释：
从第一个数组选择[9]，从第二个数组选择[8, 9]
```


 ### 参考代码
 考点：
* 贪心

题解：
* 首先取k个数字，分别从两个部分取，所以枚举从两个部分取出数字的数量。
* 当前数组要取k个数时，贪心的每次将数组前面的数字和尾部比较，尾部较小时，删去即可，直至尾部大于当前时插入。
* 当两个数组分别选择完毕后，再进入选择，每次比较两数组的大小，取大的数组数组的头部，最后返回列表，然后结束后和当前答案比较更新。
```python
class Solution:
    # @param {int[]} nums1 an integer array of length m with digits 0-9
    # @param {int[]} nums2 an integer array of length n with digits 0-9
    # @param {int} k an integer and k <= m + n
    # @return {int[]} an integer array
    def maxNumber(self, nums1, nums2, k):
        # Write your code here
        len1, len2 = len(nums1), len(nums2)
        res = []
        for x in range(max(0, k - len2), min(k, len1) + 1):
            tmp = self.merge(self.getMax(nums1, x), self.getMax(nums2, k - x))
            res = max(tmp, res)
        return res

    def getMax(self, nums, t):
        ans = []
        size = len(nums)
        for x in range(size):
            while ans and len(ans) + size - x > t and ans[-1] < nums[x]:
                ans.pop()
            if len(ans) < t:
                ans.append(nums[x])
        return ans

    def merge(self, nums1, nums2):
        return [max(nums1, nums2).pop(0) for _ in nums1 + nums2]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
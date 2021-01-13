# 山脉序列中的最大值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-number-in-mountain-sequence/?utm_source=sc-github-wzz)
 ## 题目描述
 给 `n` 个整数的山脉数组，即先增后减的序列，找到山顶（最大值）
 ### 样例说明
 例1:
```
输入: nums = [1, 2, 4, 8, 6, 3] 
输出: 8
```
例2:
```
输入: nums = [10, 9, 8, 7], 
输出: 10
```

 ### 参考代码
 二分法，判断山脉趋势，按照取数递归左边或者右边即可。
山顶的条件是第一个使得 `nums[i] > nums[i + 1]` 的 i。
当然也可以反过来，最后一个使得 `nums[i] > nums[i - 1]` 的 i
```
[[python]]
class Solution:
    """
    @param nums: a mountain sequence which increase firstly and then decrease
    @return: then mountain top
    """
    def mountainSequence(self, nums):
        if not nums:
            return -1
            
        # find first index i so that nums[i] > nums[i + 1]
        start, end = 0, len(nums) - 1
        while start + 1 < end:
            mid = (start + end) // 2
            # mid + 1 保证不会越界
            # 因为 start 和 end 是 start + 1 < end
            if nums[mid] > nums[mid + 1]:
                end = mid
            else:
                start = mid
        
        return max(nums[start], nums[end])
[[java]]
public class Solution {
    /**
     * @param nums: a mountain sequence which increase firstly and then decrease
     * @return: then mountain top
     */
    public int mountainSequence(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
            
        // find first index i so that nums[i] > nums[i + 1]
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = (start + end) / 2;
            // mid + 1 保证不会越界
            // 因为 start 和 end 是 start + 1 < end
            if (nums[mid] > nums[mid + 1]) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        return Math.max(nums[start], nums[end]);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
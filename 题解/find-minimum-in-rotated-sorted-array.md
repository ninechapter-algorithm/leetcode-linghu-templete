# 寻找旋转排序数组中的最小值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 假设一个排好序的数组在其某一未知点发生了旋转（比如`0 1 2 4 5 6 7` 可能变成`4 5 6 7 0 1 2`）。你需要找到其中最小的元素。
 ### 样例说明
 **样例 1:**
```
输入：[4, 5, 6, 7, 0, 1, 2]
输出：0
解释：
数组中的最小值为0
```

**样例 2:**
```
输入：[2,1]
输出：1
解释：
数组中的最小值为1
```
 ### 参考代码
 第二种解法，每次都和 end 去比。
```
[[python]]
class Solution:
    """
    @param: nums: a rotated sorted array
    @return: the minimum number in the array
    """
    def findMin(self, nums):
        if not nums:
            return -1
            
        start, end = 0, len(nums) - 1
        while start + 1 < end:
            mid = (start + end) // 2
            if nums[mid] > nums[end]:
                start = mid
            else:
                end = mid
                
        return min(nums[start], nums[end])
[[java]]
public class Solution {
    /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] > nums[end]) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        return Math.min(nums[start], nums[end]);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
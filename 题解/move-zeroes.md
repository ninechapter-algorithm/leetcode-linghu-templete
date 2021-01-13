# 移动零
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/move-zeroes/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个数组 *nums* 写一个函数将 `0` 移动到数组的最后面，非零元素保持原数组的顺序
 ### 样例说明
 例1:
```
输入: nums = [0, 1, 0, 3, 12],
输出: [1, 3, 12, 0, 0].
```
例2:
```
输入: nums = [0, 0, 0, 3, 1],
输出: [3, 1, 0, 0, 0].
```


 ### 参考代码
 这个版本可以保证最小的“写”次数。
```
[[python]]
class Solution:
    """
    @param nums: an integer array
    @return: nothing
    """
    def moveZeroes(self, nums):
        left, right = 0, 0
        while right < len(nums):
            if nums[right] != 0:
                if left != right:
                    nums[left] = nums[right]
                left += 1
            right += 1
            
        while left < len(nums):
            if nums[left] != 0:
                nums[left] = 0
            left += 1
[[java]]
public class Solution {
    /**
     * @param nums: an integer array
     * @return: nothing
     */
    public void moveZeroes(int[] nums) {
        int left = 0, right = 0;
        while (right < nums.length) {
            if (nums[right] != 0) {
                if (left != right) {
                    nums[left] = nums[right];
                }
                left++;
            }
            right++;
        }
        while (left < nums.length) {
            if (nums[left] != 0) {
                nums[left] = 0;
            }
            left++;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 两数之和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-sum-greater-than-target/?utm_source=sc-github-wzz)
 ## 题目描述
 给一组整数，问能找出多少对整数，他们的和大于一个给定的目标值。
 ### 样例说明
 **样例 1:**

```
输入: [2, 7, 11, 15], target = 24
输出: 1
解释: 11 + 15 是唯一的一对
```

**样例 2:**

```
输入: [1, 1, 1, 1], target = 1
输出: 6
```
 ### 参考代码
 总体思路是排序后使用两根指针进行遍历, 而遍历的过程有多种实现方式.

本题解采用的思路是:

- 定义左右端点指针`l = 0`, `r = n - 1` (n是数组长度)
- 若 `l` 指向元素与 `r` 指向元素的和不大于 `target`, 则 `l` 右移; 反之, `result += r - l`, 并 `r` 左移
- 终止条件为 `l >= r`

上述思路利用了单调性: 若 `nums[l] + nums[r] > target`, 则 `nums[l + k] + nums[r] > target (k >= 0)`

`result += r - l` 代表 `nums[r]` 可以与 `nums[l], nums[l + 1], ... , nums[r - 1]` 这 `r - l` 个元素成对, 加和大于 `target`.

一个小优化: `l` 左移时可以用二分/倍增加速.
```java
public class Solution {
    /**
     * @param nums: an array of integer
     * @param target: an integer
     * @return: an integer
     */
    public int twoSum2(int[] nums, int target) {
        if (nums == null || nums.length < 2) {
            return 0;
        }
        
        Arrays.sort(nums);
        
        int left = 0, right = nums.length - 1;
        int count = 0;
        while (left < right) {
            if (nums[left] + nums[right] <= target) {
                left++;
            } else {
                count += right - left;
                right--;
            }
        }
        
        return count;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
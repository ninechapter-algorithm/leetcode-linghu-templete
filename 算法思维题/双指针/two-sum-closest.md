# 两数和的最接近值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-sum-closest/?utm_source=sc-github-wzz)
 ## 题目描述
 给定整数数组`num`，从中找到两个数字使得他们和最接近`target`，返回两数和与 `target` 的差的 `绝对值`。
 ### 样例说明
 
 ### 参考代码
 将数组排序后，双指针求解
第一个指针初始位置在最前面，从前往后走
第二个指针初始位置在最后面，从后往前走，
在这个过程中迭代更新答案
```java
public class Solution {
    /**
     * @param nums an integer array
     * @param target an integer
     * @return the difference between the sum and the target
     */
    public int twoSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 2) {
            return -1;
        }
        
        Arrays.sort(nums);
        
        int left = 0, right = nums.length - 1;
        int diff = Integer.MAX_VALUE;
        
        while (left < right) {
            if (nums[left] + nums[right] < target) {
                diff = Math.min(diff, target - nums[left] - nums[right]);
                left++;
            } else {
                diff = Math.min(diff, nums[left] + nums[right] - target);
                right--;
            }
        }
        
        return diff;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
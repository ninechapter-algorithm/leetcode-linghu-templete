# 两数和-小于或等于目标值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-sum-less-than-or-equal-to-target/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，找出这个数组中有多少对的和是小于或等于目标值。返回对数。
 ### 样例说明
 例1:
```
输入: nums = [2, 7, 11, 15], target = 24. 
输出: 5. 
解释:
2 + 7 < 24
2 + 11 < 24
2 + 15 < 24
7 + 11 < 24
7 + 15 < 24
```

例2:
```
输入: nums = [1], target = 1. 
输出: 0. 
```


 ### 参考代码
 排序后双指针即可。
```java
public class Solution {
    /**
     * @param nums an array of integer
     * @param target an integer
     * @return an integer
     */
    public int twoSum5(int[] nums, int target) {
        // Write your code here
        if (nums == null || nums.length < 2)
            return 0;

        Arrays.sort(nums);
        int cnt = 0;
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int v = nums[left] + nums[right];
            if (v > target) {
                right --;
            } else {
                cnt += right - left;
                left ++;
            }
        }
        return cnt;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
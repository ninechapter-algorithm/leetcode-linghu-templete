# 和大于S的最小子数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-size-subarray-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个由 `n` 个正整数组成的数组和一个正整数 `s` ，请找出该数组中满足其和 ≥ s 的最小长度子数组。如果无解，则返回 -1。

 ### 样例说明
 **样例 1:**

```
输入: [2,3,1,2,4,3], s = 7
输出: 2
解释: 子数组 [4,3] 是该条件下的最小长度子数组。
```

**样例 2:**

```
输入: [1, 2, 3, 4, 5], s = 100
输出: -1
```
 ### 参考代码
 用两根指针对数组进行一次遍历即可.

如果当前和小于`s`, 右指针右移, 扩大区间, 反之左指针右移, 缩小区间.

在这个过程中维持区间的和不小于`s`, 然后更新答案即可.
```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @param s: an integer
     * @return: an integer representing the minimum size of subarray
     */
    public int minimumSize(int[] nums, int s) {
        // write your code here
        int sum = 0;
        int ans = Integer.MAX_VALUE;

        for (int l = 0, r = 0; r < nums.length; r++) {
            sum += nums[r];

            while (sum >= s) {
                ans = Math.min(ans, r - l + 1);
                sum -= nums[l++];
            }
        }

        return ans == Integer.MAX_VALUE ? -1 : ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
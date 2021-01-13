# 子数组的最大平均值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-average-subarray/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个由`n`个整数组成的数组，找到给定长度`k`的连续子数组，该子数组具有最大平均值。你需要输出最大平均值。
 ### 样例说明
 **样例1**

```
输入: nums = [1,12,-5,-6,50,3] and k = 4
输出: 12.75
解释:
最大平均为(12-5-6+50)/4 = 51/4 = 12.75
```



**样例2**

```
输入: nums = [4,2,1,3,3] and k = 2
输出: 3.00
解释:
最大平均为(3+3)/2 = 6/2 = 3.00
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param nums: an array
     * @param k: an integer
     * @return: the maximum average value
     */
    public double findMaxAverage(int[] nums, int k) {
        // Write your code here
        int n = nums.length;
        int[] sum = new int[n + 1];
        for(int i = 1; i <= n; i++){
            sum[i] = sum[i - 1] + nums[i - 1];
        }
        int ans = Integer.MIN_VALUE;
        for(int i = k; i <= n; i++){
            ans = Math.max(ans, sum[i] - sum[i - k]);
        }
        return ans * 1.0 / k;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
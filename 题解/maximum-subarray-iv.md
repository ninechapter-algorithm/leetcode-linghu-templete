# 最大子序列的和IV
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-subarray-iv/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，找到长度大于或等于 `k` 的连续子序列使它们的和最大，返回这个最大的和，如果数组中少于k个元素则返回 `0`
 ### 样例说明
 例1:
```
输入:
[-2,2,-3,4,-1,2,1,-5,3]
5
输出:
5
解释:
[2,-3,4,-1,2,1]
sum=5
```

例2:
```
输入:
[5,-10,4]
2
输出:
-1
```


 ### 参考代码
 一维dp即可。
维护一个前缀和。
再维护一个前缀合法最小和，
转移方程如下：
 result = Math.max(result, sum[i] - min_prefix)
min_prefix = Math.min(min_prefix, sum[i - k + 1])
```java
public class Solution {
    /**
     * @param nums an array of integers
     * @param k an integer
     * @return the largest sum
     */
    public int maxSubarray4(int[] nums, int k) {
        // Write your code here
        int n = nums.length;
        if (n < k)
            return 0;

        int result = 0;
        for (int i = 0; i < k; ++i)
            result += nums[i];

        int[] sum = new int[n + 1];
        sum[0] = 0;
        
        int min_prefix = 0;
        for (int i = 1; i <= n; ++i) {
            sum[i] = sum[i - 1] + nums[i - 1];
            if (i >= k && sum[i] - min_prefix > result) {
                result = Math.max(result, sum[i] - min_prefix);
            }
            if (i >= k) {
                min_prefix = Math.min(min_prefix, sum[i - k + 1]);
            }
        }
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
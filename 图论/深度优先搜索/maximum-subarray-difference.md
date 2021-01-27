# 最大子数组差
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-subarray-difference/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个整数数组，找出两个<b><font color="#e76363">不重叠</font></b>的子数组A和B，使两个子数组和的差的绝对值<strong style="line-height: 1.42857143; font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;"><font color="#e76363">|SUM(A) - SUM(B)|</font></strong><span style="line-height: 1.42857143;">最大。</span></p><p>返回这个最大的差值。</p>
 ### 样例说明
 
例1:
```
输入:[1, 2, -3, 1]
输出:6
解释:
子数组是 [1,2] 和[-3].所以答案是 6.
```

例2:
```
输入:[0,-1]
输出:1
解释:
子数组是 [0] 和 [-1].所以答案是 1.
```



 ### 参考代码
 dp。
维护四个数组，当前位置左边的最大子数组和，最小子数组和。当前位置右边的最大子数组和，最小子数组和。
然后枚举分割线，扫描一下即可。
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer indicate the value of maximum difference between two
     *          Subarrays
     */
    public int maxDiffSubArrays(int[] nums) {
        // write your code here
        int size = nums.length;
        int[] left_max = new int[size];
        int[] left_min = new int[size];
        int[] right_max = new int[size];
        int[] right_min = new int[size];
        int[] copy = new int[size];
        /*Get negative copy*/
        for(int i = 0; i < size; i++){
            copy[i] = -1 * nums[i];
        }
        int max = Integer.MIN_VALUE;
        int sum = 0;
        int minSum = 0;
        /*Forward: get max subarray*/
        for(int i = 0; i < size; i++){
            sum += nums[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(sum, minSum);
            left_max[i] = max;
        }
        /*Backward: get max subarray*/
        max = Integer.MIN_VALUE;
        sum = 0;
        minSum = 0;
        for(int i = size - 1; i >= 0; i--){
            sum += nums[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(sum, minSum);
            right_max[i] = max;
        }
        /*Forward: get min subarray*/
        max = Integer.MIN_VALUE;
        sum = 0;
        minSum = 0;
        for(int i = 0; i < size; i++){
            sum += copy[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(sum, minSum);
            left_min[i] = -1 * max;
        }
        /*Backward: get min subarray*/
        max = Integer.MIN_VALUE;
        sum = 0;
        minSum = 0;
        for(int i = size - 1; i >= 0; i--){
            sum += copy[i];
            max = Math.max(max, sum - minSum);
            minSum = Math.min(sum, minSum);
            right_min[i] = -1 * max;
        }
        int diff = 0;
        for(int i = 0; i < size - 1; i++){
            diff = Math.max(diff, Math.abs(left_max[i] - right_min[i + 1]));
            diff = Math.max(diff, Math.abs(left_min[i] - right_max[i + 1]));
        }
        return diff;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
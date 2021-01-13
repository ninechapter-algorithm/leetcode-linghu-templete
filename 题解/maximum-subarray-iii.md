# 最大子数组 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-subarray-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组和一个整数 *k*，找出 *k* 个**不重叠**子数组使得它们的和最大。每个子数组的数字在数组中的位置应该是**连续**的。

返回最大的和。
 ### 样例说明
 **样例1**

```plain
输入: 
List = [1,2,3]
k = 1
输出: 6
说明: 1 + 2 + 3 = 6
```

**样例2**

```plain
输入:
List = [-1,4,-2,3,-2,3]
k = 2
输出: 8
说明: 4 + (3 + -2 + 3) = 8
```


 ### 参考代码
 DP: an array partition into k parts or k operation (like buy and sell stock)
Use local max and global max
$localMax[n][k]$ defines max sum, must have nth element for n and partition into k parts.
$globalMax[n][k]$ defines max sum, may not have nth element for n and partition into k parts.
```java
// 方法一 划分类DP
public class Solution {
    /**
     * @param nums: A list of integers
     * @param k: An integer denote to find k non-overlapping subarrays
     * @return: An integer denote the sum of max k non-overlapping subarrays
     */
    public int maxSubArray(int[] nums, int k) {
        if (nums.length < k) {
            return 0;
        }
        int len = nums.length;
        
       
        int[][] globalMax = new int[k + 1][len + 1];
        int[][] localMax = new int[k + 1][len + 1];
        
        for (int i = 1; i <= k; i++) {
            localMax[i][i-1] = Integer.MIN_VALUE;
            //小于 i 的数组不能够partition
            for (int j = i; j <= len; j++) {
                localMax[i][j] = Math.max(localMax[i][j-1], globalMax[i - 1][j-1]) + nums[j-1];
                if (j == i)
                    globalMax[i][j] = localMax[i][j];
                else
                    globalMax[i][j] = Math.max(globalMax[i][j-1], localMax[i][j]);
            }
        }
        return globalMax[k][len];
    }
    
}


//方法二
public class Solution {
    /**
     * @param nums: A list of integers
     * @param k: An integer denote to find k non-overlapping subarrays
     * @return: An integer denote the sum of max k non-overlapping subarrays
     */ 
    public static int maxSubArray(ArrayList<Integer> nums, int k) {
        // write your code
        int len = nums.size();
        int[][] f = new int[k+1][len];
        for (int i = 1; i < k+1; i++) {
            int sum = 0;
            for (int j = 0; j < i; j++) {
                sum += nums.get(j);
            }
            f[i][i-1] = sum;
        }
        for (int i = 1; i < len; i++) {
        	f[1][i] = Math.max(f[1][i-1]+nums.get(i), nums.get(i));
        }
        
        for (int i = 2; i < k+1; i++) {
            for (int n = i;  n< len; n++) {
                int curMax = f[i][n-1] + nums.get(n);
                for (int j = i-2; j < n; j++) {
                    if ((f[i-1][j] + nums.get(n)) > curMax) {
                        curMax = f[i-1][j] + nums.get(n);
                    }
                }
                f[i][n] = curMax;
            }
        }
        
        int res = Integer.MIN_VALUE;
        for (int i = k-1; i < len; i++){
            if (f[k][i] > res) {
                res = f[k][i];
            }
        }
        return res;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
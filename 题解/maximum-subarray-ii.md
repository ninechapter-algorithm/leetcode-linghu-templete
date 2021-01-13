# 最大子数组 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-subarray-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，找出两个 *不重叠* 子数组使得它们的和最大。
每个子数组的数字在数组中的位置应该是连续的。
返回最大的和。
 ### 样例说明
 
例1:
```
输入:
[1, 3, -1, 2, -1, 2]
输出:
7
解释:
最大的子数组为 [1, 3] 和 [2, -1, 2] 或者 [1, 3, -1, 2] 和 [2].
```

例2:
```
输入:
[5,4]
输出:
9
解释:
最大的子数组为 [5] 和 [4].
```

 ### 参考代码
 <p style="color: rgb(113, 113, 113); font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;"></p><p>这个题的思路是，因为 两个subarray 一定不重叠</p><p><span style="background-color: initial;">所以必定存在一条分割线</span><br></p><p><span style="background-color: initial;">分开这两个 subarrays</span><br></p><p><span style="background-color: initial;">所以 最后的部分里：</span><br></p><p>&nbsp; max = Integer.MIN_VALUE;</p><p>&nbsp; &nbsp; &nbsp; &nbsp; for(int i = 0; i &lt; size - 1; i++){</p><p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; max = Math.max(max, left[i] + right[i + 1]);</p><p>&nbsp; &nbsp; &nbsp; &nbsp; }</p><p>&nbsp; &nbsp; &nbsp; &nbsp; return max;</p><p>这里是在枚举 这条分割线的位置</p><p><span style="background-color: initial;">然后 left[] 和 right[] 里分别存的是，某个位置往左的 maximum subarray 和往右的 maximum subarray</span><br></p><p style="color: rgb(113, 113, 113); font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;"></p>

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer denotes the sum of max two non-overlapping subarrays
     */
    public int maxTwoSubArrays(ArrayList<Integer> nums) {
        // write your code
        int size = nums.size();
        int[] left = new int[size];
        int[] right = new int[size];
        int sum = 0;
        int minSum = 0;
        int max = Integer.MIN_VALUE;
        for(int i = 0; i < size; i++){
            sum += nums.get(i);
            max = Math.max(max, sum - minSum);
            minSum = Math.min(sum, minSum);
            left[i] = max;
        }
        sum = 0;
        minSum = 0;
        max = Integer.MIN_VALUE;
        for(int i = size - 1; i >= 0; i--){
            sum += nums.get(i);
            max = Math.max(max, sum - minSum);
            minSum = Math.min(sum, minSum);
            right[i] = max;
        }
        max = Integer.MIN_VALUE;
        for(int i = 0; i < size - 1; i++){
            max = Math.max(max, left[i] + right[i + 1]);
        }
        return max;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 乘积最大子序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-product-subarray/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>找出一个序列中乘积最大的连续子序列（至少包含一个数）。</p>
 ### 样例说明
 **样例 1:**
```
输入:[2,3,-2,4]
输出:6
```

**样例 2:**
```
输入:[-1,2,4,1]
输出:8
```
 ### 参考代码
 ## 算法：dp
比较容易想出来的线性dp。由于数据中有正有负，所以我们利用两个dp数组来完成。用f[i]来保存计算到第i个时的最大值，用g[i]来保持计算到第i个时的最小值。
- 在得出了第i-1的dp值之后，即包含i-1的可能值区间为[g[i-1],f[i-1]]（左闭右闭区间）。我们考虑第i个数的情况。
- 若nums[i]为正数，可能值区间为[g[i-1]×nums[i],f[i-1]×nums[i]]，和nums[i]。
- 若nums[i]为负数，可能值区间为[f[i-1]×nums[i],g[i-1]×nums[i]]，和nums[i]。
- 所以我们直接根据上述的情况，就能得出包含nums[i]的最大值f[i]=max(max(f[i-1]×nums[i], g[i-1]×nums[i]), nums[i])。同理，g[i]=min(min(f[i-1]*×[i], g[i-1]×nums[i]), nums[i])。
- 最后由于我们要求的是最大值，直接对f数组取最大值即可。

## 复杂度分析
* 时间复杂度`O(n)`
  * 枚举了数组的长度 
* 空间复杂度`O(n)`
  * 消耗了等长的空间
```java
// LeetCode version:
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: an integer
     */
    public int maxProduct(List<Integer> nums) {
        int[] max = new int[nums.size()];
        int[] min = new int[nums.size()];
        
        min[0] = max[0] = nums.get(0);
        int result = nums.get(0);
        for (int i = 1; i < nums.size(); i++) {
            min[i] = max[i] = nums.get(i);
            if (nums.get(i) > 0) {
                max[i] = Math.max(max[i], max[i - 1] * nums.get(i));
                min[i] = Math.min(min[i], min[i - 1] * nums.get(i));
            } else if (nums.get(i) < 0) {
                max[i] = Math.max(max[i], min[i - 1] * nums.get(i));
                min[i] = Math.min(min[i], max[i - 1] * nums.get(i));
            }
            
            result = Math.max(result, max[i]);
        }
        
        return result;
    }
}

// LintCode Version 1:
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: an integer
     */
    public int maxProduct(int[] nums) {
        int[] max = new int[nums.length];
        int[] min = new int[nums.length];
        
        min[0] = max[0] = nums[0];
        int result = nums[0];
        for (int i = 1; i < nums.length; i++) {
            min[i] = max[i] = nums[i];
            if (nums[i] > 0) {
                max[i] = Math.max(max[i], max[i - 1] * nums[i]);
                min[i] = Math.min(min[i], min[i - 1] * nums[i]);
            } else if (nums[i] < 0) {
                max[i] = Math.max(max[i], min[i - 1] * nums[i]);
                min[i] = Math.min(min[i], max[i - 1] * nums[i]);
            }
            
            result = Math.max(result, max[i]);
        }
        
        return result;
    }
}

//LintCode version2: O(1) Space Complexity
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: an integer
     */
    public int maxProduct(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int minPre = nums[0], maxPre = nums[0];
        int max = nums[0], min = nums[0];
        int res = nums[0];
        for (int i = 1; i < nums.length; i ++) {
            max = Math.max(nums[i], Math.max(maxPre * nums[i], minPre * nums[i]));
            min = Math.min(nums[i], Math.min(maxPre * nums[i], minPre * nums[i]));
            res = Math.max(res, max);
            maxPre = max;
            minPre = min;
        }
        return res;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
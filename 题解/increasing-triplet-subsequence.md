# 递增的三元子序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/increasing-triplet-subsequence/?utm_source=sc-github-wzz)
 ## 题目描述
 给定未排序的数组，返回是否在数组中存在递增的长度为3的子序列。

完整的功能应为：
如果存在i, j, k，使得arr[i] < arr[j] < arr[k]，且0 ≤ i < j < k ≤ n-1，则返回true，否则返回false。
您的算法应该以O(n)时间复杂度和O(1)空间复杂度运行。
 ### 样例说明
 **样例1**
```
输入： [1, 2, 3, 4, 5]
输出： true
```
**样例2**
```
输入： [5, 4, 3, 2, 1]
输出： false
```
 ### 参考代码
 直接遍历一遍数组，用一个维护一个最小值以及次小值，如果当前值小于最小值则更新最小值，若大于最小值小于次小值则更新次小值，若大于次小值则返回true。
```java
// O(n) memory, if you want O(1)memory take a look at the c++ version
public class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums.length < 2)
            return false;
        int n = nums.length;
        boolean []has_first_small = new boolean[n];
        int smallest = nums[0];
        has_first_small[0] = false;
        for (int i = 0; i < n; i ++) {
            if (smallest < nums[i]) {
                has_first_small[i] = true;
            }
            smallest = Math.min(smallest, nums[i]);
        }
        
        int biggest = nums[n-1];
        for (int i = n-2; i >=0; i--) {
            if(has_first_small[i] == true) {
                if (nums[i] < biggest) {
                    return true;
                }
                biggest = Math.max(biggest, nums[i]);
            }
        }
        return false;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
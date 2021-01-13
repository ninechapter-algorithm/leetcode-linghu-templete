# 数组第二大数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/second-max-of-array/?utm_source=sc-github-wzz)
 ## 题目描述
 在数组中找到第二大的数。
 ### 样例说明
 例1：
```
输入：[1,3,2,4]
输出：3
```
例2：
```
输入：[1,1,2,2]
输出：2
```
 ### 参考代码
 维护最大数和此大数即可
```java
public class Solution {
    /**
     * @param nums: An integer array.
     * @return: The second max number in the array.
     */
    public int secondMax(int[] nums) {
        int max = Math.max(nums[0], nums[1]);
        int second = Math.min(nums[0], nums[1]);
        
        for (int i = 2; i < nums.length; i++) {
            if (nums[i] > max) {
                second = max;
                max = nums[i];
            } else if (nums[i] > second) {
                second = nums[i];
            }
        }
        
        return second;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 划分和相等的子集
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/partition-equal-subset-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给一 `只含有正整数` 的 `非空` 数组, 找到这个数组是否可以划分为 `两个` 元素和相等的子集。
 ### 样例说明
 例1:
```
输入: nums = [1, 5, 11, 5], 
输出: true
解释:
two subsets: [1, 5, 5], [11]
```
例2:
```
输入: nums = [1, 2, 3, 9], 
输出: false
```

 ### 参考代码
 等价与背包问题，能否背到总价值的一半。
01背包即可。
```java
public class Solution {
    public boolean canPartition(int[] nums) {
        int len = nums.length;
        int sum = 0;
        for(int i = 0; i < len ; i++ ){
            sum += nums[i];
        }
        if(sum % 2 == 1){
            return false;
        }
        sum /= 2;
        boolean [] dp = new boolean[20000];
        for(int i = 0; i <=sum ; i ++)
            dp[i] = false;
        dp[0] = true;
        for(int i = 0; i < len; i++){
            for(int j= sum ; j >= nums[i]; j--){
                dp[j] |= dp[j - nums[i]];
            }
        }
        return dp[sum];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 删除并赚取
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/delete-and-earn/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，你可以在这个数组上进行操作。

在每次操作中，你可以选择任意数num[i]并且删除它从而得到num[i]的分数。在此之后，你必须删除掉任何和num[i]-1或者num[i]+1相等的元素。

你将从0分开始。返回你通过这些操作可以获得的最大的分数。
 ### 样例说明
 ```
样例 1:
	输入:  nums = [3, 4, 2]
	输出:  6
	
	解释:
	删除4，获得4分。同时删除3
	然后删除2，获得2分。

	
样例 2:
	输入: nums = [2, 2, 3, 3, 3, 4]
	输出:  9
	
	解释:
	删除3，获得3分。然后删除2和4
	然后再删除3，获得3分。
	再删除3，获得3分。
	
```
 ### 参考代码
 DP[i]表示删除的数字不超过i时所能获得的最大的分数。

考虑当前数字是主动删的还是被动删的。
由于i-1和i+1是相互的，我们只考虑一边，避免重复。
```java
class Solution {
    public int deleteAndEarn(int[] nums) {
        int[] counters = new int[10001];
        for (int i = 0; i < nums.length; i++) {
            counters[nums[i]]++;
        }
        
        int[] dp = new int[10001];
        dp[1] = counters[1];
        for (int i = 2; i <= 10000; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + i * counters[i]);
        }
        
        return dp[10000];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
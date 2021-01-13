# 目标和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/target-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个非负整数的列表a1,a2,...an，再给定一个目标S。现在用`+`和`-`两种运算，对于每一个整数，选择一个作为它前面的符号。

找出有多少种方法，使得这些整数的和正好等于S。
 ### 样例说明
 例1:
```
输入: nums为 [1, 1, 1, 1, 1], S 为 3. 
输出: 5
解释: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

有5种方法让和为3.
```

例2:
```
输入: nums 为 [], S 为 3. 
输出: 0
解释: 
没有方法能让和为3
```

 ### 参考代码
 用DFS搜索所有的可能，或利用动态规划记录状态来搜索
```java
// DP 解法
public class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        int sum = 0;
        for (int a : nums) {
            sum += a;
        }
        if (sum < Math.abs(S)) {
            return 0;
        }

        //init for dp
        int doubleSum = sum << 1;
        int[][] dp = new int[nums.length][doubleSum + 1];
        if (nums[0] == 0) {
            dp[0][sum] = 2;
        } else {
            dp[0][sum - nums[0]] = 1;
            dp[0][sum + nums[0]] = 1;
        }

        //dp
        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j <= doubleSum; j++) {
                if (j - nums[i] >= 0) {
                    dp[i][j] += dp[i - 1][j - nums[i]];
                }
                if (j + nums[i] <= doubleSum) {
                    dp[i][j] += dp[i - 1][j + nums[i]];
                }
            }
        }

        return dp[nums.length - 1][S + sum];
    }
}

// DFS解法
public class Solution {
    int answer = 0;

    public int findTargetSumWays(int[] nums, int S) {
        int[] s = new int[nums.length];
        s[nums.length - 1] = nums[nums.length - 1];
        for (int i = nums.length - 2; i >= 0; i--) {
            s[i] = s[i + 1] + nums[i];
        }

        dfsHelper(nums, S, 0, 0, s);
        return answer;
    }

    public void dfsHelper(int[] nums, int S, int index, int currSum, int[] s) {
        if (index == nums.length) {
            if (currSum == S) {
                answer++;
            }
        } else if (Math.abs(S - currSum) <= s[index]) {
            dfsHelper(nums, S, index + 1, currSum + nums[index], s);
            dfsHelper(nums, S, index + 1, currSum - nums[index], s);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
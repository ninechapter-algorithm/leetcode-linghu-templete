# 最长上升子序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-increasing-subsequence/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数序列，找到最长上升子序列（LIS），返回LIS的长度。
 ### 样例说明
 ```
样例 1:
	输入:  [5,4,1,2,3]
	输出:  3
	
	解释:
	LIS 是 [1,2,3]


样例 2:
	输入: [4,2,4,5,3,7]
	输出:  4
	
	解释: 
	LIS 是 [2,4,5,7]
```
 ### 参考代码
 使用动态规划计算 Longest Increasing Subsequence，并同时打印具体的方案
```
[[python]]
class Solution:
    """
    @param nums: The integer array
    @return: The length of LIS (longest increasing subsequence)
    """
    def longestIncreasingSubsequence(self, nums):
        if nums is None or not nums:
            return 0
        
        # state: dp[i] 表示从左到右跳到i的最长sequence 的长度
        
        # initialization: dp[0..n-1] = 1
        dp = [1] * len(nums)
        
        # prev[i] 代表 dp[i] 的最优值是从哪个 dp[j] 算过来的
        prev = [-1] * len(nums)
        
        # function dp[i] = max{dp[j] + 1},  j < i and nums[j] < nums[i]
        for i in range(len(nums)):
            for j in range(i):
                if nums[j] < nums[i] and dp[i] < dp[j] + 1:
                    dp[i] = dp[j] + 1
                    prev[i] = j
        
        # answer: max(dp[0..n-1])
        longest, last = 0, -1
        for i in range(len(nums)):
            if dp[i] > longest:
                longest = dp[i]
                last = i
        
        path = []
        while last != -1:
            path.append(nums[last])
            last = prev[last]
        print(path[::-1])
        
        return longest
[[java]]
public class Solution {
    /**
     * @param nums: An integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    public int longestIncreasingSubsequence(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        } 
        int n = nums.length;
        
        // state: 
        // dp[i] 表示从左到右跳到i的最长sequence 的长度
        // prev[i] 代表 dp[i] 的最优值是从哪个 dp[j] 算过来的
        int[] prev = new int[n];
        int[] dp = new int[n];
        
        // initialization: dp[0..n-1] = 1
        for (int i = 0; i < n; i++) {
            dp[i] = 1;
            prev[i] = -1;
        }
        
        // function dp[i] = max{dp[j] + 1},  j < i and nums[j] < nums[i]
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i] && dp[j] + 1 > dp[i]) {
                    dp[i] = dp[j] + 1;
                    prev[i] = j;
                }
            }
        }
        
        // answer: max(dp[0..n-1])
        int longest = 0, last = -1;
        for (int i = 0; i < n; i++) {
            if (dp[i] > longest) {
                longest = dp[i];
                last = i;
            }
        }
        
        // print solution
        ArrayList<Integer> path = new ArrayList();
        while (last != -1) {
            path.add(nums[last]);
            last = prev[last];
        }
        for (int i = path.size() - 1; i >= 0; i--) {
            System.out.print(path.get(i) + "-");
        }
        
        return longest;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
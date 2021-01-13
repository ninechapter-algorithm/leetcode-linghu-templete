# 子数组和为K II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/subarray-sum-equals-to-k-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组和一个整数k，你需要找到和为k的最短子数组，并返回它的长度。

如果没有这样的子数组，返回-1.
 ### 样例说明
 
 ### 参考代码
 使用 前缀和+哈希表 的方法
《九章算法面试高频题冲刺班》中有讲解

```
[[python]]
class Solution:
    """
    @param nums: a list of integer
    @param k: an integer
    @return: return an integer, denote the minimum length of continuous subarrays whose sum equals to k
    """
    def subarraySumEqualsKII(self, nums, k):
        prefix_sum = self.get_prefix_sum(nums)
        
        answer = float('inf')
        sum2index = {0: 0}
        for end in range(len(nums)):
            # find prefix_sum[end + 1] - prefix_sum[start] = k
            # => prefix_sum[start] = prefix_sum[end + 1] - k
            if prefix_sum[end + 1] - k in sum2index:
               length = end + 1 - sum2index[prefix_sum[end + 1] - k] 
               answer = min(answer, length)
            sum2index[prefix_sum[end + 1]] = end + 1
            
        return answer
        
    def get_prefix_sum(self, nums):
        prefix_sum = [0]
        for num in nums:
            prefix_sum.append(prefix_sum[-1] + num)
        return prefix_sum
[[java]]
public class Solution {
    /**
     * @param nums: a list of integer
     * @param k: an integer
     * @return: return an integer, denote the minimum length of continuous subarrays whose sum equals to k
     */
    public int subarraySumEqualsKII(int[] nums, int k) {
        int[] prefixSum = getPrefixSum(nums);
        
        int answer = Integer.MAX_VALUE;
        Map<Integer, Integer> sum2index = new HashMap<>();
        sum2index.put(0, 0);
        for (int end = 0; end < nums.length; end++) {
            // find prefix_sum[end + 1] - prefix_sum[start] = k
            // => prefix_sum[start] = prefix_sum[end + 1] - k
            if (sum2index.containsKey(prefixSum[end + 1] - k)) {
                int len = end + 1 - sum2index.get(prefixSum[end + 1] - k);
                answer = Math.min(answer, len);
            }
            sum2index.put(prefixSum[end + 1], end + 1);
        }
        return answer;
    }
    
    private int[] getPrefixSum(int[] nums) {
        int[] prefixSum = new int[nums.length + 1];
        prefixSum[0] = 0;
        for (int i = 0; i < nums.length; i++) {
            prefixSum[i + 1] = prefixSum[i] + nums[i];
        }
        return prefixSum;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
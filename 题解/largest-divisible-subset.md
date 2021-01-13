# 最大整除子集
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/largest-divisible-subset/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个由 `无重复的正整数` 组成的集合，找出满足任意两个元素 `(Si, Sj)` 都有 `Si % Sj = 0` 或 `Sj % Si = 0` 成立的最大子集
 ### 样例说明
 
 ### 参考代码
 dp。
首先排序。
f[i]代表以nums[i]为最大元素的序列最多有多少个。
然后只要nums[k]%nums[i]=0，则可尝试往f[k]转移。
但由于时间复杂度为O(N^2), 无法通过，需要进一步优化。
```java
public class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        Arrays.sort(nums);
        int[] f = new int[nums.length];
        int[] pre = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            f[i] = 1;
            pre[i] = i;
            for (int j = 0; j < i; j++) {
                if (nums[i] % nums[j] == 0 && f[i] < f[j] + 1) {
                    f[i] = f[j] + 1;
                    pre[i] = j;
                }
            }
        }
        
        List<Integer> ans = new ArrayList<Integer>();
        if (nums.length == 0) {
            return ans;
        }
        int max = 0;
        int max_i = 0;
        for (int i = 0; i < nums.length; i++) {
            if (f[i] > max) {
                max = f[i];
                max_i = i;
            }
        }
        ans.add(nums[max_i]);
        while (max_i != pre[max_i]) {
            max_i = pre[max_i];
            ans.add(nums[max_i]);
        }
        Collections.reverse(ans);
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
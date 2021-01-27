# 组合总和 IV
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/combination-sum-iv/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个都是正整数的数组 `nums`，其中没有重复的数。从中找出所有的和为 `target` 的组合个数。
 ### 样例说明
 **样例1**

```
输入: nums = [1, 2, 4] 和 target = 4
输出: 6
解释:
可能的所有组合有：
[1, 1, 1, 1]
[1, 1, 2]
[1, 2, 1]
[2, 1, 1]
[2, 2]
[4]
```

**样例2**

```
输入: nums = [1, 2] 和 target = 4
输出: 5
解释:
可能的所有组合有：
[1, 1, 1, 1]
[1, 1, 2]
[1, 2, 1]
[2, 1, 1]
[2, 2]
```
 ### 参考代码
 ```cpp
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        int n = nums.size();
        int f[target+1];
        memset(f, 0, sizeof(f));
        
        f[0] = 1;
        for (int i = 1; i <= target; i++) {
            for (int j = 0; j < n; j++) 
            if (i - nums[j] >= 0){
                f[i] += f[i-nums[j]];
            }
        }
        return f[target];
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
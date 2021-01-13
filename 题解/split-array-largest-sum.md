# 拆分子数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/split-array-largest-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个由非负整数组成的数组和一个整数m，我们要把数组拆分为m个非空连续子数组。编写算法以最小化这些m个子阵列中的最大总和。
 ### 样例说明
 **样例 1:**
```
输入：[7,2,5,10,8], m = 2
输出：18
解释：
    将nums拆分成子数组的方式有4种。
    最好的选择是拆分成 [7,2,5] 和 [10,8], 
    两个子数组中的最大的和只有 18。
```

**样例 2:**
```
输入：[1,4,4], m = 3
输出：4
解释：
    将nums拆分成子数组的方式有1种。
    最好的选择是拆分成 [1],[4] 和 [4],
    两个子数组中的最大的和只有4。
```



 ### 参考代码
 考点：
* 二分法

题解：二分答案即可，左端为max，右端为sum(数组和)，二分答案check即可。
```cpp
class Solution {
public:
    bool check(int max_val, vector<int>& nums, int m) {
        int cnt = 1;
        int sum = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] > max_val) {
                return false;
            }
            if (sum + nums[i] > max_val) {		//如果当前连续和大于max_val
                cnt++;							//计数+1
                sum = nums[i];					//sum更新为num[i]
            } else {
                sum += nums[i];
            }
        }
        return cnt <= m;
    }
    int splitArray(vector<int>& nums, int m) {
        long long l = 0, r = 0;
        for (int i = 0; i < nums.size(); ++i) {
            l = max((int)l, nums[i]);		//确定二分查找的左右端点
            r += nums[i];
        }
        int ans = 0;
        while(l <= r) {
            long long mid = (l + r) / 2;
            if (check(mid, nums, m)) {	//二分check
                ans = mid;
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return ans;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
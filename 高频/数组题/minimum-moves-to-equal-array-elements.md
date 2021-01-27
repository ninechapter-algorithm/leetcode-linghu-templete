# 使数组元素相同的最少步数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-moves-to-equal-array-elements/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个大小为`n`的**非空**整数数组，找出使得数组中所有元素相同的最少步数，其中一步被定义为将数组中`n - 1`个元素加一。
 ### 样例说明
 ```
输入：
[1,2,3]

输出：
3

说明：
只需要三步即可（每一步将其中两个元素加一）：

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```
 ### 参考代码
 ```cpp
class Solution {
public:
    int minMoves(vector<int>& nums) {
        int sumNum = 0;
        int minNum = INT_MAX;
        for (int num : nums) {
            sumNum += num;
            minNum = min(minNum, num);
        }
        return sumNum - minNum * nums.size();
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
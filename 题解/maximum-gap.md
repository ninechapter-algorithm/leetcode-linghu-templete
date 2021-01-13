# 最大间距
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-gap/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个未经排序的数组, 请找出这个数组排序之后的两个相邻元素之间最大的间距.

如果数组中少于 2 个元素, 返回 0.
 ### 样例说明
 **样例 1:**

```
输入: [1, 9, 2, 5]
输出: 4
解释: 排序之后的数组是 [1, 2, 5, 9], 最大的间距是在 5 和 9 之间.
```

**样例 2:**

```
输入: [1]
输出: 0
解释: 数组中的元素少于 2 个.
 ### 参考代码
 很多人用基数排序(桶排序)做这道题目, 时间复杂度接近线性, 当然比基于比较的快速排序等一众 O(nlogn) 的算法要优秀一些, 但是这道题可以有更巧妙的方法.

首先我们定义 maxNum 和 minNum 表示这个数组的最大/最小元素, N 表示这个数组元素的个数. 那么这个数组一共有 N - 1 个间距.

这 N - 1 个间距的平均值就是 avgGap = (maxNum - minNum) / (N - 1), 这个平均值也是答案的最小值. 因为这 N 个元素平均分配时, 最大的间距最小.

然后我们**对这 N 个元素分类, 分类依据就是这个元素与 minNum 的间距是 avgGap 的多少倍**. 为什么这样分类呢? 因为这样分类, **同一组内的元素的间距必然不会是最大间距**. 

这时我们要找的**最大间距处于组与组之间, 即某一组里最小的元素与它上一组的最大的元素的间距的最大值**. 因此, 我们只需要**维护每一组里最小与最大的元素**即可.

设定 maxNums 和 minNums 数组, maxNums[i] 表示原数组中与 minNum 的差为 avgGap 的 i 倍(向下取整)的最大的元素, 同理 minNums[i] 表示相同含义下的最小的元素.

然后我们遍历 maxNums, minNums, 将第 i 组的最小值 minNums[i] 与第 i - 1 组的最大值 maxNums[i - 1] 做差, 维护最大值就可以得到答案了.
```cpp
class Block {
public:
    int maxNum;
    int minNum;
    Block(): maxNum(INT_MIN), minNum(INT_MAX) {}
};

class Solution {
public:
    /**
     * @param nums: an array of integers
     * @return: the maximun difference
     */
    int maximumGap(vector<int> &nums) {
        int N = nums.size();
        int maxNum = nums[0];
        int minNum = nums[0];
        for (int num : nums) {
            maxNum = max(num, maxNum);
            minNum = min(num, minNum);
        }
        if (N < 2 || maxNum == minNum) {
            return 0;
        }
        
        vector<Block> blocks(N);
        
        int avgGap = ceil(double(maxNum - minNum) / (N - 1));
        
        for (int num : nums) {
            if (num == maxNum || num == minNum) {
                continue;
            }
            int pos = (num - minNum) / avgGap;
            blocks[pos].minNum = min(num, blocks[pos].minNum);
            blocks[pos].maxNum = max(num, blocks[pos].maxNum);
        }
        
        int maxGap = 0;
        int lastMax = minNum;
        for (int i = 0; i < N; i++) {
            if (blocks[i].minNum == INT_MAX || blocks[i].maxNum == INT_MIN) {
                continue;
            }
            maxGap = max(blocks[i].minNum - lastMax, maxGap);
            lastMax = blocks[i].maxNum;
        }
        maxGap = max(maxNum - lastMax, maxGap);
        
        return maxGap;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
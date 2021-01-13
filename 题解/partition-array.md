# 数组划分
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/partition-array/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个整数数组 *nums* 和一个整数 *k*。划分数组（即移动数组 *nums* 中的元素），使得：

- 所有小于k的元素移到左边
- 所有大于等于k的元素移到右边

返回数组划分的位置，即数组中第一个位置 *i*，满足 *nums*[*i*] 大于等于 *k*。
 ### 样例说明
 例1:
```
输入:
[],9
输出:
0

```

例2:
```
输入:
[3,2,2,1],2
输出:1
解释:
真实的数组为[1,2,2,3].所以返回 1
```


 ### 参考代码
 快速选择算法
```python
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: As description
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        left, right = 0, len(nums) - 1
        while left <= right:
            while left <= right and nums[left] < k:
                left += 1
            while left <= right and nums[right] >= k:
                right -= 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        return left
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
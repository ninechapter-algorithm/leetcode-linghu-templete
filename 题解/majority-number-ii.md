# 主元素 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/majority-number-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个整型数组，找到主元素，它在数组中的出现次数严格大于数组元素个数的三分之一。</p><p><br></p>
 ### 样例说明
 
 ### 参考代码
 可以发现，对于其他的元素来讲，若出现次数大于1/3，则两者出现总次数大于2/3.必不可能被抵消。
若其他元素出现次数均不超过1/3，可以发现，抵消与重建至少要2/3的花费，则这个出现次数大于1/3的数必出现在candidate1与candidate2中，不可能被替换掉。
```python
class Solution:
    """
    @param nums: A list of integers
    @return: The majority number occurs more than 1/3
    """
    def majorityNumber(self, nums):
        candidate1, count1 = None, 0
        candidate2, count2 = None, 0
        for num in nums:
            if candidate1 == num:
                count1 += 1
            elif candidate2 == num:
                count2 += 1
            elif count1 == 0:
                count1 += 1
                candidate1 = num
            elif count2 == 0:
                count2 += 1
                candidate2 = num
            else:
                count1 -= 1
                count2 -= 1
    
        count1, count2 = 0, 0
        for num in nums:
            if candidate1 == num:
                count1 += 1
            elif candidate2 == num:
                count2 += 1
    
        return candidate1 if count1 > count2 else candidate2
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
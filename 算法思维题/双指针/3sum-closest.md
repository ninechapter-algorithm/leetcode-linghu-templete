# 最接近的三数之和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/3sum-closest/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个包含 *n* 个整数的数组 *S*, 找到和与给定整数 *target* 最接近的三元组，返回这三个数的和。
 ### 样例说明
 例1:
```
输入:[2,7,11,15],3
输出:20
解释:
2+7+11=20
```

例2:
```
输入:[-1,2,1,-4],1
输出:2
解释:
-1+2+1=2
```

 ### 参考代码
 排序后。
固定一个点，利用双指针的方式，扫描，记录答案即可。
```python
class Solution:
    """
    @param numbers: Give an array numbers of n integer
    @param target: An integer
    @return: return the sum of the three integers, the sum closest target.
    """
    def threeSumClosest(self, numbers, target):
        numbers.sort()
        ans = None
        for i in range(len(numbers)):
            left, right = i + 1, len(numbers) - 1
            while left < right:
                sum = numbers[left] + numbers[right] + numbers[i]
                if ans is None or abs(sum - target) < abs(ans - target):
                    ans = sum
                    
                if sum <= target:
                    left += 1
                else:
                    right -= 1
        return ans
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
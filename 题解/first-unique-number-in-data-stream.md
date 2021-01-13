# 数据流中第一个唯一的数字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/first-unique-number-in-data-stream/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个连续的数据流,写一个函数返回终止数字到达时的第一个唯一数字（包括终止数字）,如果找不到这个终止数字, 返回 `-1`.
 ### 样例说明
 **样例1**
```
输入： 
[1, 2, 2, 1, 3, 4, 4, 5, 6]
5
输出： 3
```
**样例2**
```
输入：
[1, 2, 2, 1, 3, 4, 4, 5, 6]
7
输出： -1
```
**样例3**
```
输入：
[1, 2, 2, 1, 3, 4]
3
输出： 3
```
 ### 参考代码
 如果允许遍历两次，简单的这么做就可以了
如果只允许遍历一次，请参见 first unique number in data stream ii 这个题的参考答案
```python
class Solution:
    """
    @param nums: a continuous stream of numbers
    @param number: a number
    @return: returns the first unique number
    """
    def firstUniqueNumber(self, nums, number):
        counter = {}
        for num in nums:
            counter[num] = counter.get(num, 0) + 1
            if num == number:
                break
        else:
            return -1
            
        for num in nums:
            if counter[num] == 1:
                return num
            if num == number:
                break

        return -1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 上一个排列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/previous-permutation/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组来表示排列，找出其上一个排列。
 ### 样例说明
 
例1:
```
输入:[1]
输出:[1]
```


例2:
```
输入:[1,3,2,3]
输出:[1,2,3,3]
```

例3:
```
输入:[1,2,3,4]
输出:[4,3,2,1]

```

 ### 参考代码
 从排列的最末尾开始，找到第一个下降点，下降点的意义为这个点之前的序列无需改动。
然后,将后面的序列变为降序。
从下降点开始扫描，找到第一个比她小的数字，交换即可。
```python
class Solution:
    # @param num :  a list of integer
    # @return : a list of integer
    def previousPermuation(self, num):
        # write your code here
        for i in range(len(num)-2, -1, -1):
            if num[i] > num[i+1]:
                break
        else:
            num.reverse()
            return num
        for j in range(len(num)-1, i, -1):
            if num[j] < num[i]:
                num[i], num[j] = num[j], num[i]
                break
        for j in range(0, (len(num) - i)//2):
            num[i+j+1], num[len(num)-j-1] = num[len(num)-j-1], num[i+j+1]
        return num
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
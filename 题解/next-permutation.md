# 下一个排列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/next-permutation/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组来表示排列，找出其之后的一个排列。
 ### 样例说明
 例1:
```
输入:[1]
输出:[1]
```


例2:
```
输入:[1,3,2,3]
输出:[1,3,3,2]
```

例3:
```
输入:[4,3,2,1]
输出:[1,2,3,4]
```

 ### 参考代码
 从最后一个位置开始，找到一个上升点，上升点之前的无需改动。
然后，翻转上升点之后的降序。
在降序里，找到第一个比上升点大的，交换位置。
```python
class Solution:
    # @param num :  a list of integer
    # @return : a list of integer
    def nextPermutation(self, num):
        # write your code here
        for i in range(len(num)-2, -1, -1):
            if num[i] < num[i+1]:
                break
        else:
            num.reverse()
            return num
        for j in range(len(num)-1, i, -1):
            if num[j] > num[i]:
                num[i], num[j] = num[j], num[i]
                break
        for j in range(0, (len(num) - i)//2):
            num[i+j+1], num[len(num)-j-1] = num[len(num)-j-1], num[i+j+1]
        return num
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
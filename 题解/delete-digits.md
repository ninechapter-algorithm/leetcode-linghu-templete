# 删除数字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/delete-digits/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个字符串 *A*, 表示一个 *n* 位正整数, 删除其中 *k* 位数字, 使得剩余的数字仍然按照原来的顺序排列产生一个新的正整数。

找到删除 *k* 个数字之后的最小正整数。

*N* <= 240, *k* <= *N*

 ### 样例说明
 **样例 1：**
```
输入: A = "178542", k = 4
输出:"12"
```

**样例 2：**
```
输入: A = "568431", k = 3
输出:"431"
```
 ### 参考代码
 ```python
class Solution:
    """
    @param A: A positive integer which has N digits, A is a string.
    @param k: Remove k digits.
    @return: A string
    """
    def DeleteDigits(self, A, k):
        # write you code here
        A = list(A)
        while k > 0:
            f = True
            for i in xrange(len(A)-1):
                if A[i] > A[i+1]:
                    del A[i]
                    f = False
                    break	 
            if f and len(A)>1:
                A.pop()
            k -= 1
        while len(A)>1 and A[0]=='0':
            del A[0]
        return ''.join(A)   
 

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
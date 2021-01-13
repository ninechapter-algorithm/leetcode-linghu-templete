# UTF-8编码检查
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/utf-8-validation/?utm_source=sc-github-wzz)
 ## 题目描述
 UTF-8编码中，一个字符的长度可以是**1到4字节**，服从如下的规则：

1. 对于单字节的字符，第`1`位是一个`'0'`，后续二进制位为其unicode编码。
2. 对于`n`字节的字符，第一个字节的前`n`位全是`'1'`，第`n+1`位是`'0'`；对于后续的`n-1`字节，每个字节最高两位是`'10'`。

以下是字符编号范围与UTF-8编码对应表：
```
       字符编号范围     |        UTF-8编码的八位组序列
      (十六进制形式)    |            (二进制形式)
   --------------------+---------------------------------------------
   0000 0000-0000 007F | 0xxxxxxx
   0000 0080-0000 07FF | 110xxxxx 10xxxxxx
   0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx
   0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
```
给定一个用来表示数据的整数数组，判断其是否为一个合法的UTF-8编码。
 ### 样例说明
 **样例1**
```
输入：[197, 130, 1]
输出：true
解释：
[197, 130, 1]，它代表的八位组序列为：11000101 10000010 00000001。
这是一个合法的utf-8编码，在双字节编码的字符之后跟了一个单字节编码的字符。
```
**样例2**
```
输入：[235, 140, 4]
输出：false
解释：
[235, 140, 4]，它代表的八位组序列为：11101011 10001100 00000100。
前三位都是'1'，第四位是'0'说明这是一个三字节编码的字符。
第二个字节是一个后续的字节，它以"10"起始，此处没问题。
但是第三个字节，也就是第二个后续的字节没有从"10"起始，所以这个编码不合法。
```
 ### 参考代码
 这个题目主要是需要理解题面的意思。
题目中给出的数组是一串二进制编码，他可能是由多个字符构成的，因此逐个字符去判断合理性即可。
```python
def check(nums, start, size):
    for i in range(start + 1, start + size + 1):
        if i >= len(nums) or (nums[i] >> 6) != 0b10:
            return False
    return True

class Solution(object):
    def validUtf8(self, nums, start=0):
        while start < len(nums):
            first = nums[start]
            if (first >> 3) == 0b11110 and check(nums, start, 3):
                start += 4
            elif (first >> 4) == 0b1110  and check(nums, start, 2): 
                start += 3
            elif (first >> 5) == 0b110   and check(nums, start, 1): 
                start += 2
            elif (first >> 7) == 0:
                start += 1
            else:
                return False
        return True
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 比较字符串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/compare-strings/?utm_source=sc-github-wzz)
 ## 题目描述
 比较两个字符串A和B，确定A中是否包含B中所有的字符。字符串A和B中的字符都是 **大写字母**
 ### 样例说明
 给出 A = `"ABCD"` B = `"ACD"`，返回 `true`

给出 A = `"ABCD"`  B = `"AABC"`， 返回 `false`
 ### 参考代码
 ```python
class Solution:
    """
    @param A : A string includes Upper Case letters
    @param B : A string includes Upper Case letters
    @return :  if string A contains all of the characters in B return True else return False
    """
    def compareStrings(self, A, B):
        # write your code here
        if len(B) == 0:
            return True
        if len(A) == 0:
            return False
        #trackTable首先记录A中所有的字符以及它们的个数，然后遍历B,如果出现trackTable[i]小于0的情况，说明B中该字符出现的次数
        #大于在A中出现的次数
        trackTable = [0 for _ in range(26)]
        for i in A:
            trackTable[ord(i) - 65] += 1
        for i in B:
            if trackTable[ord(i) - 65] == 0:
                return False
            else:
                trackTable[ord(i) -65] -= 1
        return True
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
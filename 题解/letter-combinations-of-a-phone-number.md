# 电话号码的字母组合
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/letter-combinations-of-a-phone-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个不包含`0`和`1`的数字字符串，每个数字代表一个字母，请返回其所有可能的字母组合。

下图的手机按键图，就表示了每个数字可以代表的字母。

1|2<br />ABC|3<br />DEF
:--:|:--:|:--:
**4**<br />**GHI**|**5**<br />**JKL**|**6**<br />**MNO**
**7**<br />**PQRS**|**8**<br />**TUV**|**9**<br />**WXYZ**
 ### 样例说明
 **样例 1:**

```
输入: "23"
输出: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
解释: 
'2' 可以是 'a', 'b' 或 'c'
'3' 可以是 'd', 'e' 或 'f'
```

**样例 2:**

```
输入: "5"
输出: ["j", "k", "l"]
```
 ### 参考代码
 使用深度优先搜索算法。
```
KEYBOARD = {
    '2': 'abc',
    '3': 'def',
    '4': 'ghi',
    '5': 'jkl',
    '6': 'mno',
    '7': 'pqrs',
    '8': 'tuv',
    '9': 'wxyz',
}

class Solution:
    """
    @param digits: A digital string
    @return: all posible letter combinations
    """
    def letterCombinations(self, digits):
        if not digits:
            return []
            
        results = []
        self.dfs(digits, 0, [], results)
        
        return results
    
    def dfs(self, digits, index, chars, results):
        if index == len(digits):
            results.append(''.join(chars))
            return
        
        for letter in KEYBOARD[digits[index]]:
            chars.append(letter)
            self.dfs(digits, index + 1, chars, results)
            chars.pop()
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# Excel表列标题
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/excel-sheet-column-title/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个正整数，返回相应的列标题，如Excel表中所示。
 ### 样例说明
 **样例1**

```
输入: 28
输出: "AB"
```

**样例2**

```
输入: 29
输出: "AC"
```
 ### 参考代码
 ```cpp
class Solution {
public:
    string convertToTitle(int n) {
        if (n == 0) {
            return "";
        }
        return convertToTitle((n - 1) / 26) + (char)((n - 1) % 26 + 'A');
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
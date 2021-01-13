# NULL 结尾的字符串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/null-terminated-string/?utm_source=sc-github-wzz)
 ## 题目描述
 用 C 或 C++ 设计一个 void reverse `(char* str)` 功能，实现把一个以 NULL 结尾字符串翻转的功能。
 ### 样例说明
 
 ### 参考代码
 首尾双指针，依次交换，直至相遇。
```cpp
class Solution {
public:
    /**
     * @param str C-String
     * @return void
     */
    void reverse(char *str) {
        // Write your code here
        char * end = str;
        char tmp;
        if (str) {
            while (*end != NULL) {
                ++end;
            }
        }
        --end;
        while (str < end) {
            tmp = *str;
            *str++ = *end;
            *end-- = tmp;
        }
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
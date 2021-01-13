# 交换不借助额外变量(仅C++)
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/swap-without-extra-variable-only-c/?utm_source=sc-github-wzz)
 ## 题目描述
 给出两个变量，x 和 y ，不使用第三个变量交换这两个变量的值。
 ### 样例说明
 **样例 1:**
```
输入 : x = 10, y = 5
输出 : x = 5, y = 10
```
 ### 参考代码
 通过位运算实现。
```cpp
class Solution {
public:
    /**
     * @param x an integer
     * @param y an integer
     * @return nothing
     */
    void swap(int &x, int &y) {
        // Write your code here
        x = x ^ y;
        y = x ^ y;
        x = x ^ y;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# O(1)时间检测2的幂次
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/o1-check-power-of-2/?utm_source=sc-github-wzz)
 ## 题目描述
 用 O(*1*) 时间检测整数 *n* 是否是 *2* 的幂次。
 ### 样例说明
 
 ### 参考代码
 2的幂的数字，其二进制中只有一个1。
$n&(n-1) == 0$ 说明只有1个1。
```cpp
class Solution {
public:
    /*
     * @param n: An integer
     * @return: True or false
     */
    bool checkPowerOf2(int n) {
        // write your code here
        if (n==0)
            return false;
        while (n % 2 == 0)
            n /=2 ;
        return n == 1;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
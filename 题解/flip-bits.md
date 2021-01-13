# 将整数A转换为B
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/flip-bits/?utm_source=sc-github-wzz)
 ## 题目描述
 如果要将整数n转换为m，需要改变多少个bit位？
 ### 样例说明
 
 ### 参考代码
 a ^ b 得到的结果的二进制中，1的个数就是a和b相异的位数。
```java
class Solution {
    /**
     *@param a, b: Two integer
     *return: An integer
     */
    public static int bitSwapRequired(int a, int b) {
        // write your code here
        int count = 0;  
        for (int c = a ^ b; c != 0; c = c >>> 1) {
            count += c & 1;
        }
        return count;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
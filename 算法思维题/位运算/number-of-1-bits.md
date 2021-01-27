# 判断一个整数中有多少个1
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/number-of-1-bits/?utm_source=sc-github-wzz)
 ## 题目描述
 写一个函数，其以无符号整数为输入，而输出对应二进制数所具有的“1”的位数（也被称为汉明权重）
 ### 样例说明
 **样例 1**
```
输入：n = 11
输出：3
解析：11(10) = 1011(2), 返回 3
```
**样例 2**
```
输入：n = 7
输出：3
解析：7(10) = 111(2), 返回 3
```
 ### 参考代码
 使用位运算符号‘&’，与1做与操作
并将n右移一位( >>1 )
直到n为0
```java
public class Solution {
    /**
     * @param n: an unsigned integer
     * @return: the number of â€™1' bits
     */
    public int hammingWeight(int n) {
        int ones = 0;
        while(n!=0) {
            ones += (n & 1);
            n = n>>1;
        }
        return ones;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
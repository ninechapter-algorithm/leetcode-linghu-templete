# 颠倒二进制位
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reverse-bits/?utm_source=sc-github-wzz)
 ## 题目描述
 颠倒给定的 32 位无符号整数的二进制位。
 ### 样例说明
 **样例 1:**
```
输入: 00000010100101000001111010011100
输出: 00111001011110000010100101000000
解释: 
输入的二进制串 00000010100101000001111010011100 表示无符号整数 43261596，
因此返回 964176192，其二进制表示形式为 00111001011110000010100101000000。
```
**样例 2:**
```
输入：11111111111111111111111111111101
输出：10111111111111111111111111111111
解释：
输入的二进制串 11111111111111111111111111111101 表示无符号整数 4294967293，
因此返回 3221225471 其二进制表示形式为 10101111110010110010011101101001。
```
 ### 参考代码
 分离出输入数字的每一位，最低位左移31bit，次低位左移30bit，以此类推。
```java
public class Solution {
    // you need treat n as an unsigned value
    public long reverseBits(int n) {
        int reversed = 0;
        for (int i = 0; i < 32; i++) {
            reversed = (reversed << 1) | (n & 1);
            n = (n >> 1);
        }
        return reversed;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
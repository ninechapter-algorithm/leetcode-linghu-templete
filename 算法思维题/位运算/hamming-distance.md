# Hamming距离
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/hamming-distance/?utm_source=sc-github-wzz)
 ## 题目描述
 两个整数的Hamming距离是对应比特位不同的个数。
给定两个整数x和y，计算两者的Hamming距离。
 ### 样例说明
 **样例1**

```
输入: x = 1 和 y = 4
输出: 2
解释:
1的二进制表示是001
4的二进制表示是100
共有2位不同
```



**样例2**

```
输入: x = 5 和 y = 2
输出: 3
解释:
5的二进制表示是101
2的二进制表示是010
共有3位不同
```
 ### 参考代码
 ```java
public class Solution {
    public int hammingDistance(int x, int y) {
        int Distance=0;
        
        while ( x != 0 || y != 0 ) {
            if ( x % 2 != y % 2 ) {
                Distance ++;
            }
            x /= 2;
            y /= 2;
        }
        return Distance;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
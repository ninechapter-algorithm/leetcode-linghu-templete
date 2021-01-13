# 丑数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/ugly-number/?utm_source=sc-github-wzz)
 ## 题目描述
 写一个程序来检测一个整数是不是`丑数`。

丑数的定义是，只包含质因子 `2, 3, 5` 的正整数。比如 6, 8 就是丑数，但是 14 不是丑数因为他包含了质因子 7。
 ### 样例说明
 例1:
```
输入: num = 8 
输出: true
解释:
8=2*2*2
```
例2:
```
输入: num = 14 
输出: false
解释:
14=2*7 
```

 ### 参考代码
 看这个数是否只有2，3，5的因子
```java
public class Solution {
    /**
     * @param num an integer
     * @return true if num is an ugly number or false
     */
    public boolean isUgly(int num) {
        if (num <= 0) return false;  
        if (num == 1) return true;  
          
        while (num >= 2 && num % 2 == 0) num /= 2;  
        while (num >= 3 && num % 3 == 0) num /= 3;  
        while (num >= 5 && num % 5 == 0) num /= 5;  
          
        return num == 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
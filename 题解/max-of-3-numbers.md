# 三数之中的最大值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/max-of-3-numbers/?utm_source=sc-github-wzz)
 ## 题目描述
 给三个整数，求他们中的最大值。
 ### 样例说明
 ```
样例  1:
	输入:  num1 = 1, num2 = 9, num3 = 0
	输出: 9
	
	样例解释: 
	返回三个数中最大的数。

样例 2:
	输入:  num1 = 1, num2 = 2, num3 = 3
	输出: 3
	
	样例解释: 
	返回三个中最大的数字。

```
 ### 参考代码
 if选择语句的基本操作
```java
public class Solution {
    /**
     * @param a an integer
     * @param b an integer
     * @param c an integer
     * @return an integer
     */
    public int maxOfThreeNumbers(int a, int b, int c) {
        if (a >= b && a >= c) {
            return a;
        } else if (b >= a && b >= c) {
            return b;
        } else {
            return c;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
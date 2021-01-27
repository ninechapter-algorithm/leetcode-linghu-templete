# 简单计算器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/simple-calculator/?utm_source=sc-github-wzz)
 ## 题目描述
 给出两个整数 *a* , *b* ,以及一个操作符 *opeator*
```
+, -, *, /
```
返回结果 `a<operator>b`
 ### 样例说明
 ```
样例 1:
	输入:  a = 1, b = 2, operator = +
	输出: 3
	
	样例解释: 
	返回 1 + 2 的结果.

样例 2:
	输入:  a = 10, b = 20, operator = *
	输出: 200
	
	样例解释: 
	返回10 * 20的结果.

样例 3:
	输入:  a = 3, b = 2, operator = /
	输出: 1
	
	样例解释: 
	返回 3 / 2的结果.

样例 4:
	输入:  a = 10, b = 11, operator = -
	输出: -1
	
	样例解释: 
	返回 10 - 11的结果.

```
 ### 参考代码
 简单模拟
```java
public class Calculator {
    /**
      * @param a, b: Two integers.
      * @param operator: A character, +, -, *, /.
      */
    public int calculate(int a, char operator, int b) {
        switch (operator) {
            case '+': return a + b;
            case '-': return a - b;
            case '*': return a * b;
            case '/': return a / b;
        }
        return 0;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
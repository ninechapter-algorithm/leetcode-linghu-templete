# 斐波纳契数列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/fibonacci/?utm_source=sc-github-wzz)
 ## 题目描述
 查找斐波纳契数列中第 N 个数。

所谓的斐波纳契数列是指：

- 前2个数是 0 和 1 。
- 第 *i* 个数是第 *i*-1 个数和第*i*-2 个数的和。

斐波纳契数列的前10个数字是：

`0, 1, 1, 2, 3, 5, 8, 13, 21, 34 ...`
 ### 样例说明
 ```
样例  1:
	输入:  1
	输出: 0
	
	样例解释: 
	返回斐波那契的第一个数字，是0.

样例 2:
	输入:  2
	输出: 1
	
	样例解释: 
	返回斐波那契的第二个数字是1.

```
 ### 参考代码
 纯用递归会超时，如果用带有记忆化的递归就可以，使用循环和记忆化递归的时间复杂度一样，都是$O(n)$。

不超出Integer的斐波那契数很少，仅有50个左右。
但是使用纯的递归，复杂度会是$O(2^n)$。因此会超时。
```java
class Solution {
    /**
     * @param n: an integer
     * @return an integer f(n)
     */
    public int fibonacci(int n) {
        int a = 0;
        int b = 1;
        for (int i = 0; i < n - 1; i++) {
            int c = a + b;
            a = b;
            b = c;
        }
        return a;
    }
}

//递归版本，会超时
public class Solution {
    /*
     * @param : an integer
     * @return: an ineger f(n)
     */
    public int fibonacci(int n) {
        // write your code here
        if (n == 1) {
            return 0;
        }
        
        if (n == 2) {
            return 1;
        }
        
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
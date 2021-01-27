# 分解质因数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/prime-factorization/?utm_source=sc-github-wzz)
 ## 题目描述
 将一个整数分解为若干质因数之乘积。
 ### 样例说明
 **样例 1：**
```
输入：10
输出：[2, 5]
```
**样例 2：**
```
输入：660
输出：[2, 2, 3, 5, 11]
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param num an integer
     * @return an integer array
     */
    public List<Integer> primeFactorization(int num) {
        List<Integer> factors = new ArrayList<Integer>();

        for (int i = 2; i * i <= num; i++) {
            while (num % i == 0) {
                num = num / i;
                factors.add(i);
            }
        }
        
        if (num != 1) {
            factors.add(num);
        }
        
        return factors;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
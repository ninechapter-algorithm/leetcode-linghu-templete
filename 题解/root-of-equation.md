# 方程的根
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/root-of-equation/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个方程：*a*x<sup>2</sup> + *b*x + *c* = 0，求根。

* 如果方程有两个根，就返回一个包含两个根的数组/列表。
* 如果方程只有一个根，就返回一个包含一个跟的数组/列表。
* 如果方程没有根，就返回一个空数组/列表。
 ### 样例说明
 
**样例 1：**
```
输入：a = 1, b = -2, c = 1
输出：[1]
解释：方程有一个根，返回 [1]。
```
**样例 2：**
```
输入：a = 1, b = -3, c = 2
输出：[1,2]
解释：方程有两个根，返回 [1,2] 且第一个数应比第二个数小。
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param a an integer
     * @param b an integer
     * @param c an integer
     * @return a double array
     */
    public double[] rootOfEquation(double a, double b, double c) {
        if (b * b - 4 * a * c < 0) {
            return new double[0];
        }
        
        if (b * b - 4 * a * c == 0) {
            double[] root = new double[1];
            root[0] = -b / 2.0 / a;
            return root;
        }
        
        double[] root = new double[2];
        double delta = Math.sqrt(b * b - 4 * a * c);
        root[0] = (-b - delta) / 2.0 / a;
        root[1] = (-b + delta) / 2.0 / a;
        
        if (root[0] > root[1]) {
            double temp = root[0];
            root[0] = root[1];
            root[1] = temp;
        }
        return root;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
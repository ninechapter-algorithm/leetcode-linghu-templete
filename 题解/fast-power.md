# 快速幂
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/fast-power/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>计算<b style="color: rgb(113, 113, 113); font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;"><font color="#e76363"><i>a<span style="position: relative; font-size: 12px; line-height: 0; vertical-align: baseline; top: -0.5em;">n</span>&nbsp;% b</i></font></b><span style="line-height: 1.42857143;">，</span><span style="line-height: 1.42857143;">其中a，b和n都是32位的非负整数。</span></p>
 ### 样例说明
 <p style="font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;"><font color="#424242">例如 2<span style="position: relative; font-size: 12px; line-height: 0; vertical-align: baseline; top: -0.5em;">31</span>&nbsp;% 3 = 2</font></p><p style="font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;"><font color="#424242">例如 100<span style="position: relative; font-size: 12px; line-height: 0; vertical-align: baseline; top: -0.5em;">1000</span>&nbsp;% 1000 = 0</font></p>
 ### 参考代码
 ```java
class Solution {
    /*
     * @param a, b, n: 32bit integers
     * @return: An integer
     */
    public int fastPower(int a, int b, int n) {
        if (n == 1) {
            return a % b;
        }
        if (n == 0) {
            return 1 % b;
        }
        
        long product = fastPower(a, b, n / 2);
        product = (product * product) % b;
        if (n % 2 == 1) {
            product = (product * a) % b;
        }
        return (int) product;
    }
};

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
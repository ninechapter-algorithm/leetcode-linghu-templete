# 水仙花数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/narcissistic-number/?utm_source=sc-github-wzz)
 ## 题目描述
 水仙花数的定义是，这个数等于他每一位数上的幂次之和 [见维基百科的定义](https://en.wikipedia.org/wiki/Narcissistic_number "See wiki")

比如一个3位的十进制整数`153`就是一个水仙花数。因为 153 = 1<sup>3</sup> + 5<sup>3</sup> + 3<sup>3</sup>。

而一个4位的十进制数`1634`也是一个水仙花数，因为 1634 = 1<sup>4</sup> + 6<sup>4</sup> + 3<sup>4</sup> + 4<sup>4</sup>。

给出`n`，找到所有的n位十进制水仙花数。
 ### 样例说明
 **样例 1:**

```
输入: 1
输出: [0,1,2,3,4,5,6,7,8,9]
```

**样例 2:**

```
输入:  2
输出: []	
样例解释: 没有2位数的水仙花数。
```
 ### 参考代码
 直接枚举，拆数计算然后判断即可。
```java
class Solution {
    /*
     * @param n: The number of digits. 
     * @return: All narcissistic numbers with n digits.
     */
    public ArrayList<Integer> getNarcissisticNumbers(int n) {
        // write your code here
        ArrayList<Integer> result = new ArrayList<Integer>();
        if (n == 1) {
            for (int i = 0; i < 10; ++i)
                result.add(i);
            return result;
        }
        if (n == 6) {
            result.add(548834);
            return result;
        }

        for (int i = pow(10, n-1); i < pow(10, n); ++i) {
            int j = i;
            int s = 0;
            while (j > 0) {
                s += pow((j % 10), n);
                j = j / 10;
            }
            if (s == i)
                result.add(i);
        }
        return result;
    }
    
    public int pow(int a, int b) {
        int val = 1;
        for (int i = 1; i <=b; ++i)
            val *=a;
        return val;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
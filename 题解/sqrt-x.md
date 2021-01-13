# 对x开根
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sqrt-x/?utm_source=sc-github-wzz)
 ## 题目描述
 实现 `int sqrt(int x)` 函数，计算并返回 *x* 的平方根。

 ### 样例说明
 
 ### 参考代码
 Implement int sqrt(int x).

Compute and return the square root of x.
<div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博: &nbsp;</span><font color="#666e70" face="Open Sans, Arial, sans-serif"><span style="line-height: 22.3999996185303px;"><a href="http://weibo.com/3948019741/BDJCsFUbt" target="_blank">http://weibo.com/3948019741/BDJCsFUbt</a></span></font><br></div>
```java
class Solution {
    /**
     * @param x: An integer
     * @return: The sqrt of x
     */
    public int sqrt(int x) {
        // find the last number which square of it <= x
        long start = 1, end = x;
        while (start + 1 < end) {
            long mid = start + (end - start) / 2;
            if (mid * mid <= x) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (end * end <= x) {
            return (int) end;
        }
        return (int) start;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 数组的最大值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/max-of-array/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个浮点数数组，求数组中的最大值。
 ### 样例说明
 **样例 1:**

```
输入:  [1.0, 2.1, -3.3]
输出: 2.1	
样例解释: 返回最大的数字
```
**样例 2:**

```
输入:  [1.0, 1.0, -3.3]
输出: 1.0	
样例解释: 返回最大的数字。
```
 ### 参考代码
 模拟过程
```java
public class Solution {
    /**
     * @param A a float array
     * @return a float number
     */
    public float maxOfArray(float[] A) {
        float max = A[0];
        for (int i = 1; i < A.length; i++) {
            if (A[i] > max) {
                max = A[i];
            }
        }
        return max;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 数组剔除元素后的乘积
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/product-of-array-exclude-itself/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组A。
定义`B[i] = A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]`， 计算B的时候请不要使用除法。请输出B。
 ### 样例说明
 **样例 1**
```
输入: A = [1, 2, 3]
输出: [6, 3, 2]
解析：B[0] = A[1] * A[2] = 6; B[1] = A[0] * A[2] = 3; B[2] = A[0] * A[1] = 2
```
**样例 2**
```
输入: A = [2, 4, 6]
输出: [24, 12, 8]
```
 ### 参考代码
 分两次循环
第一次记录数组从后往前的累乘结果，f[i]代表i位之后所有元素的乘积
第二次循环，从左往右，跳过 i 左侧累乘，右侧直接乘以f[i + 1]
```java
import java.util.ArrayList;

public class Solution {
    /**
     * @param nums: Given an integers array A
     * @return: A Long array B and B[i]= A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]
     */
    public ArrayList<Long> productExcludeItself(ArrayList<Integer> A) {
        int len = A.size();
        ArrayList<Long> B = new  ArrayList<Long>();
        long[] f = new long[len];

        long tmp = 1;
        long now = 1;
        f[len-1] = A.get(len-1);
        int i ;
        for ( i = len-2; i >= 0; --i)
        {
            f[i] = A.get(i);
            f[i] = f[i] * f[i+1];
        }

        for ( i = 0; i < len; ++i) {
			
            now = tmp;
            if(i+1<len)
                B.add( now * f[i+1] );
            else
                B.add( now );
            now = A.get(i);
            tmp = tmp * now;

        }
        return B;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
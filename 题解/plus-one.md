# 加一
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/plus-one/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个非负数，表示一个数字数组，在该数的基础上+1，返回一个新的数组。

该数字按照数位高低进行排列，最高位的数在列表的最前面。
 ### 样例说明
 **样例 1：**
```
输入：[1,2,3]
输出：[1,2,4]
```
**样例 2：**
```
输入：[9,9,9]
输出：[1,0,0,0]
```
 ### 参考代码
 Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.
```java
public class Solution {
    // The complexity is O(1)
    // f(n) = 9/10 + 1/10 * O(n-1)
    //  ==>  O(n) =  10 / 9 = 1.1111 = O(1)
    
    public int[] plusOne(int[] digits) {
        int carries = 1;
        for(int i = digits.length-1; i>=0 && carries > 0; i--){  // fast break when carries equals zero
            int sum = digits[i] + carries;
            digits[i] = sum % 10;
            carries = sum / 10;
        }
        if(carries == 0)
            return digits;
            
        int[] rst = new int[digits.length+1];
        rst[0] = 1;
        for(int i=1; i< rst.length; i++){
            rst[i] = digits[i-1];
        }
        return rst;
    }
}


```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
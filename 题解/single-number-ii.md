# 落单的数 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/single-number-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出3*n + 1 个非负整数，除其中一个数字之外其他每个数字均出现三次，找到这个数字。</p>
 ### 样例说明
 **样例 1:**

```
输入:  [1,1,2,3,3,3,2,2,4,1]
输出:  4
```

**样例 2:**

```
输入: [2,1,2,2]
输出:  1	
```
 ### 参考代码
 Given an array of integers, every element appears three times except for one. Find that single one.&nbsp;<div><br></div><div>Note:&nbsp;</div><div>Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?<div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博：&nbsp;</span><a href="http://weibo.com/3948019741/BjVFuAKoh" target="_blank">http://weibo.com/3948019741/BjVFuAKoh</a><br></div></div>


统计二进制每个位上1的个数并对3取模。
出现一次的数字对应位上的1会被统计出来。
```java
public class Solution {
    public int singleNumberII(int[] A) {
        if (A == null || A.length == 0) {
            return -1;
        }
        int result=0;
        int[] bits=new int[32];
        for (int i = 0; i < 32; i++) {
            for(int j = 0; j < A.length; j++) {
                bits[i] += A[j] >> i & 1;
                bits[i] %= 3;
            }

            result |= (bits[i] << i);
        }
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
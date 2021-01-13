# 丢失的第一个正整数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/first-missing-positive/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个无序的整数数组，找出其中没有出现的最小正整数。
 ### 样例说明
 **样例 1:**
```
输入:[1,2,0]
输出:3
```

**样例 2:**
```
输入:[3,4,-1,1]
输出:2
```
 ### 参考代码
 Given an unsorted integer array, find the first missing positive integer.&nbsp;<div><br></div><div>For example,&nbsp;</div><div>Given [1,2,0] return 3,&nbsp;</div><div>and [3,4,-1,1] return 2.&nbsp;</div><div><br></div><div>&nbsp;Your algorithm should run in O(n) time and uses constant space.</div><div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博:&nbsp;</span><font color="#666e70" face="Open Sans, Arial, sans-serif"><span style="line-height: 22.3999996185303px;"><a href="http://weibo.com/3948019741/BDSXrEVB3" target="_blank">http://weibo.com/3948019741/BDSXrEVB3</a></span></font><br></div>
```java
public class Solution {

    public int firstMissingPositive(int[] A) {
        if (A == null) {
            return 1;
        }

        for (int i = 0; i < A.length; i++) {
            while (A[i] > 0 && A[i] <= A.length && A[i] != (i+1)) {
                int tmp = A[A[i]-1];
                if (tmp == A[i]) {
                    break;
                }
                A[A[i]-1] = A[i];
                A[i] = tmp;
            }
        }

        for (int i = 0; i < A.length; i ++) {
                if (A[i] != i + 1) {
                    return i + 1;
                }
        }

        return A.length + 1;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
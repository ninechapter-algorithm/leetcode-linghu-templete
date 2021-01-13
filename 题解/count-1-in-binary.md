# 二进制中有多少个1 
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/count-1-in-binary/?utm_source=sc-github-wzz)
 ## 题目描述
 计算在一个 32 位的整数的二进制表示中有多少个 `1`。
 ### 样例说明
 **样例 1：**
```
输入：32
输出：1
解释：
32(100000)，返回 1。
```
**样例 2：**
```
输入：5
输出：2
解释：
5(101)，返回 2。
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param num: an integer
     * @return: an integer, the number of ones in num
     */
    public int countOnes(int num) {
        int count = 0;
        while (num != 0) {
            num = num & (num - 1);
            count++;
        }
        return count;
    }
};

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
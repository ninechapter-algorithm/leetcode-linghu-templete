# 奇偶分割数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/partition-array-by-odd-and-even/?utm_source=sc-github-wzz)
 ## 题目描述
 分割一个整数数组，使得奇数在前偶数在后。

 ### 样例说明
 **样例1:**

```plain
输入: [1,2,3,4]
输出: [1,3,2,4]
```

**样例2:**

```plain
输入: [1,4,2,3,5,6]
输出: [1,3,5,4,2,6]
```


 ### 参考代码
 原题目很简单，只需要将原数组扫描两遍，第一遍加入奇数，第二遍加入偶数，然后把答案数组覆盖原数组即可。

对于challenge问题，我们需要采用双指针（two pointer）的方法，一个从头开始，一个从尾开始，头指针定位到从前到后的第一个偶数，尾指针定位到从后到前的第一个奇数，两者交换即可。直到尾指针在头之前前面。
```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: nothing
     */
    public void partitionArray(int[] nums) {
        int start = 0, end = nums.length - 1;
        while (start < end) {
            while (start < end && nums[start] % 2 == 1) {
                start++;
            }
            while (start < end && nums[end] % 2 == 0) {
                end--;
            }
            if (start < end) {
                int temp = nums[start]; nums[start] = nums[end]; nums[end] = temp;
                start++;
                end--;
            } 
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
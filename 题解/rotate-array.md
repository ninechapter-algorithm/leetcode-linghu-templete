# 旋转数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rotate-array/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个数组，将数组向右移动k步，其中k为非负数。
 ### 样例说明
 **样例 1:**
```
输入: [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转1步: [7,1,2,3,4,5,6]
向右旋转2步: [6,7,1,2,3,4,5]
向右旋转3步: [5,6,7,1,2,3,4]
```

**样例 2:**
```
输入: [-1,-100,3,99], k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转1步: [99,-1,-100,3]
向右旋转2步: [3,99,-1,-100]
```
 ### 参考代码
 Example：nums = [1,2,3,4,5,6,7] k = 3
Step1:划分成[1,2,3,4], [5,6,7]
Step2:分别reverse，[4,3,2,1], [7,6,5]
Step3:合并reverse，[5,6,7,1,2,3,4]
```java
public class Solution {
    /**
     * @param nums: an array
     * @param k: an integer
     * @return: rotate the array to the right by k steps
     */
    public int[] rotate(int[] nums, int k) {
        // Write your code here
        int n = nums.length;
        k %= n;
        reverse(nums, 0, n - k - 1);
        reverse(nums, n - k, nums.length - 1);
        reverse(nums, 0, nums.length - 1);
        return nums;
    }
    
    public void reverse(int[] n, int i, int j) {
        for (int p = i, q = j; p < q; p++, q--) {
            int temp = n[p];
            n[p] = n[q];
            n[q] = temp;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
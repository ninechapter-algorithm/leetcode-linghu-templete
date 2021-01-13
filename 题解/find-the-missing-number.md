# 寻找缺失的数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-the-missing-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个包含 0 .. *N* 中 *N* 个数的序列，找出0 .. *N* 中没有出现在序列中的那个数。
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    /**    
     * @param nums: an array of integers
     * @return: an integer
     */
    public int findMissing(int[] nums) {
        // write your code here
        int n = nums.length, i = 0;
        while (i<n) {
            while (nums[i]!=i && nums[i]<n) {
                int t = nums[i];
                nums[i] = nums[t];
                nums[t] = t;
            }
            ++i;
        }
        for (i=0; i<n; ++i)
            if (nums[i]!=i) return i;
        return n;
    }
}

//Math
public class Solution {
    /**    
     * @param nums: an array of integers
     * @return: an integer
     */
    public int findMissing(int[] nums) {
        long N = nums.length;
        long sum = N * (N + 1) / 2;
        for(int i : nums){
            sum -= i;
        }
        return (int)sum;
    }
}

//Xor
public int findMissing(int[] nums) {
    // write your code here
    int ans = 0;
    for (int i = 0; i <= nums.length; i++) {
        ans ^= i;
    }
    for (int i = 0; i < nums.length; i++) {
        ans ^= nums[i];
    }
    return ans;
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
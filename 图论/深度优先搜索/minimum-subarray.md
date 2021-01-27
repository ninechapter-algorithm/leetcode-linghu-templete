# 最小子数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-subarray/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个整数数组，找到一个具有最小和的连续子数组。返回其最小和。</p>
 ### 样例说明
 **样例 1**
```
输入：[1, -1, -2, 1]
输出：-3
```
**样例 2**
```
输入：[1, -1, -2, 1, -4]
输出：-6
```
 ### 参考代码
 定义两位数组
第一个比较大小确定当前位置的元素能否为sunArray的起点
第二个记录前 i 个元素能构成sunArray的最小和
```java
public class Solution {
    /*
     * @param nums: a list of integers
     * @return: A integer indicate the sum of minimum subarray
     */
    public int minSubArray(List<Integer> nums) {
        // write your code here
        if (nums == null || nums.size() == 0) {
            return 0;
        }
        int n = nums.size();
        int []localMin = new int[n]; 
        int []golbalMin = new int[n];
        localMin[0] = golbalMin[0] = nums.get(0);
        for(int i = 1; i < n; i++){
            localMin[i] = Math.min(localMin[i - 1] + nums.get(i), nums.get(i)); //比较判断是否从一个新的元素开始找SubArray
            golbalMin[i] = Math.min(golbalMin[i - 1], localMin[i]);// 前 i 位元素可以构成的最小subArray之和
        }
        return golbalMin[n - 1];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
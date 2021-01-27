# 连续子数组求和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/continuous-subarray-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，请找出一个连续子数组，使得该子数组的和最大。输出答案时，请分别返回第一个数字和最后一个数字的下标。（如果存在多个答案，请返回字典序最小的）
 ### 样例说明
 **样例 1:**

```
输入: [-3, 1, 3, -3, 4]
输出: [1, 4]
```

**样例 2:**

```
输入: [0, 1, 0, 1]
输出: [0, 3]
解释: 字典序最小.
```
 ### 参考代码
 枚举即可, 枚举的过程中维护以当前元素结尾的最大和.

每次循环把当前元素加到这个和中, 在加上之前判断: 

- 如果这个和是负数, 则放弃之前的元素, 把和置为0, 区间左端点设为当前元素
- 如果是正数, 则直接累加.

同时, 在枚举的过程中维护答案.

详细过程见C++注释
```java
public class Solution {
    /**
     * @param A an integer array
     * @return  A list of integers includes the index of the first number and the index of the last number
     */
    public ArrayList<Integer> continuousSubarraySum(int[] A) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        result.add(0);
        result.add(0);

        int len = A.length;
        int start = 0, end = 0;
        int sum = 0;
        int ans = -0x7fffffff;
        for (int i = 0; i < len; i++) {
            if (sum < 0) {
                sum = A[i];
                start = end = i;
            } else {
                sum += A[i];
                end = i;
            }
            if (sum > ans) {
                ans = sum;
                result.set(0, start);
                result.set(1, end);
            }
        }
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
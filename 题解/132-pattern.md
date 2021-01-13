# 132 模式
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/132-pattern/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个 n 个整数的序列 a1,a2,...,an，一个 `132` 模式是对于一个子串 ai,aj,ak，满足 `i` < `j` < `k` 和 `ai` < `ak` < `aj`。设计一个算法来检查输入的这 n 个整数的序列中是否存在132模式。
`n` 会小于 `20,000`。
 ### 样例说明
 例1:
```
输入: nums = [1, 2, 3, 4] 
输出: False 
解释:
没有132模式在这个序列中。
```
例2:
```
输入: nums = [3, 1, 4, 2] 
输出: True 
解释:
存在132模式：[1,4,2]。
```

 ### 参考代码
 s2代表当前次大值。
从最后一个开始遍历，依次与S2做比较，若小于，直接返回true，若大于，跟新s2的值即可
```java
public class Solution {
    /**
     * @param nums a list of n integers
     * @return true if there is a 132 pattern or false
     */
    public boolean find132pattern(int[] nums) {
        // Write your code here
        Stack<Integer> stack = new Stack<Integer>();
        for (int i = nums.length - 1, two = Integer.MIN_VALUE; i >= 0; i--) {
            if (nums[i] < two) {
                return true;
            } else {
                while (!stack.empty() && nums[i] > stack.peek())
                    two = stack.pop();
            }
            stack.push(nums[i]);
        }
        return false;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
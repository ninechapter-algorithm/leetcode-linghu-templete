# 132-patterns
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/132-patterns/?utm_source=sc-github-wzz)
 ## 题目描述
 1776
 ### 样例说明
 1776
 ### 参考代码
 ```java
public class Solution {
    public boolean find132pattern(int[] nums) {
        if (nums == null || nums.length < 3) {
            return false;
        }

        int[] min = new int[nums.length];
        min[0] = nums[0];

        //assign the minimum value from num[0] to num [i - 1] to min[i]
        for (int i = 1; i < nums.length; i++) {
            min[i] = Math.min(nums[i - 1], min[i - 1]);
        }

        Stack<Integer> stack = new Stack<>();
        int max = Integer.MIN_VALUE;
        for (int j = nums.length - 1; j >= 0; j--) {
            if (nums[j] > min[j]) {
                while (!stack.empty() && nums[j] > stack.peek()) {
                    max = stack.pop();
                }
                if (max > min[j]) {
                    return true;
                }
            }
            stack.push(nums[j]);
        }
        return false;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 两数之和 - 不同组成
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-sum-unique-pairs/?utm_source=sc-github-wzz)
 ## 题目描述
 给一整数数组, 找到数组中有多少组 `不同的元素对` 有相同的和, 且和为给出的 target 值, 返回对数.
 ### 样例说明
 

**例1:**
```
输入: nums = [1,1,2,45,46,46], target = 47 
输出: 2
解释:

1 + 46 = 47
2 + 45 = 47

```

**例2:**
```
输入: nums = [1,1], target = 2 
输出: 1
解释:
1 + 1 = 2
```

 ### 参考代码
 利用双指针的方法，扫描排序完的数组即可。
```java
public class Solution {
    /**
     * @param nums an array of integer
     * @param target an integer
     * @return an integer
     */
    public int twoSum6(int[] nums, int target) {
        // Write your code here
        if (nums == null || nums.length < 2)
            return 0;

        Arrays.sort(nums);
        int cnt = 0;
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int v = nums[left] + nums[right];
            if (v == target) {
                cnt ++;
                left ++;
                right --;
                while (left < right && nums[right] == nums[right + 1])
                    right --;
                while (left < right && nums[left] == nums[left - 1])
                    left ++;
            } else if (v > target) {
                right --;
            } else {
                left ++;
            }
        }
        return cnt;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
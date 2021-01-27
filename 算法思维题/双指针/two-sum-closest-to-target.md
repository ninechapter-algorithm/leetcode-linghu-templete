# 两数和的最接近值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-sum-closest-to-target/?utm_source=sc-github-wzz)
 ## 题目描述
 给定整数数组`num`，从中找到两个数字使得他们和最接近`target`，返回两数和与 `target` 的差的 `绝对值`。
 ### 样例说明
 **样例1**

```
输入: nums = [-1, 2, 1, -4] 并且 target = 4
输出: 1
解释:
最小的差距是1，(4 - (2 + 1) = 1).
```

**样例2**

```
输入: nums = [-1, -1, -1, -4] 并且 target = 4
输出: 6
解释:
最小的差距是6，(4 - (- 1 - 1) = 6).
```
 ### 参考代码
 <p>http://www.lintcode.com/problem/two-sum-closest-to-target/<br></p>
```java
public class Solution {
    /**
     * @param nums an integer array
     * @param target an integer
     * @return the difference between the sum and the target
     */
    public int twoSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 2) {
            return -1;
        }
        
        Arrays.sort(nums);
        
        int left = 0, right = nums.length - 1;
        int diff = Integer.MAX_VALUE;
        
        while (left < right) {
            if (nums[left] + nums[right] < target) {
                diff = Math.min(diff, target - nums[left] - nums[right]);
                left++;
            } else {
                diff = Math.min(diff, nums[left] + nums[right] - target);
                right--;
            }
        }
        
        return diff;
    }
}

// 九章硅谷求职算法集训营版本
public class Solution {
    /**
     * @param nums an integer array
     * @param target an integer
     * @return the difference between the sum and the target
     */
    int diff = Integer.MAX_VALUE;
    int T = 0;
    
    public void update(int[] A, int x, int y) {
        if (x != y && x >= 0 && x < A.length && y >= 0 && y < A.length) {
            diff = Math.min(diff, Math.abs(A[x] + A[y] - T));
        }
    }
    
    public int twoSumClosest(int[] A, int target) {
        // Write your code here
        T = target;
         if (A == null || A.length < 2) {
            return -1;
        }
        
        Arrays.sort(A);
        
        int j = A.length - 1;
        for (int i = 0; i < A.length; ++i) {
            while (j >= 0 && A[i] + A[j] > target) --j;
            update(A, i, j + 1);
            update(A, i, j);
            update(A, i, j - 1);
        }
        
        return diff;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
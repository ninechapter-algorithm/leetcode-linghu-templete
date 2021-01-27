# 经典二分查找问题
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/classical-binary-search/?utm_source=sc-github-wzz)
 ## 题目描述
 在一个排序数组中找一个数，返回该数出现的任意位置，如果不存在，返回 `-1`。

 ### 样例说明
 **样例 1：**
```
输入：nums = [1,2,2,4,5,5], target = 2
输出：1 或者 2
```
**样例 2：**
```
输入：nums = [1,2,2,4,5,5], target = 6
输出：-1
```
 ### 参考代码
 ```java
// version 1: with jiuzhang template
public class Solution {
    /**
     * @param A an integer array sorted in ascending order
     * @param target an integer
     * @return an integer
     */
    public int findPosition(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        return -1;
    }
}

// version 2: without jiuzhang template
public class Solution {
    /**
     * @param A an integer array sorted in ascending order
     * @param target an integer
     * @return an integer
     */
    public int findPosition(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        while (start < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        
        if (nums[start] == target) {
            return start;
        }
        return -1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 二分查找
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/first-position-of-target/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个排序的整数数组（升序）和一个要查找的整数`target`，用`O(logn)`的时间查找到target第一次出现的下标（从0开始），如果target不存在于数组中，返回`-1`。
 ### 样例说明
 ```
样例  1:
	输入:[1,4,4,5,7,7,8,9,9,10]，1
	输出: 0
	
	样例解释: 
	第一次出现在第0个位置。

样例 2:
	输入: [1, 2, 3, 3, 4, 5, 10]，3
	输出: 2
	
	样例解释: 
	第一次出现在第2个位置
	
样例 3:
	输入: [1, 2, 3, 3, 4, 5, 10]，6
	输出: -1
	
	样例解释: 
	没有出现过6， 返回-1

```
 ### 参考代码
 二分查找的模版，找第一次出现的位置。
注意可能出现多次，所以当找到这个数字的时候不能直接结束，而要将end移动到mid处。
直到最后缩小到只有一个或两个数字时，优先判断start，再判断end。

时间复杂度$O(log_2 n)$
```java
// version 1: with jiuzhang template
class Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public int binarySearch(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                end = mid;
            } else if (nums[mid] < target) {
                start = mid;
                // or start = mid + 1
            } else {
                end = mid;
                // or end = mid - 1
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
class Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public int binarySearch(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        while (start < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                end = mid;
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
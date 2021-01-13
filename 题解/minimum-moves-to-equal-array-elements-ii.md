# 使数组元素相同的最少步数 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-moves-to-equal-array-elements-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个**非空**的整数数组，找出使得数组中所有元素相同的最少步数，其中一步被定义为将数组内任一元素加一或减一。

数组中最多包含10,000个元素。
 ### 样例说明
 例1:
```
输入：
[1,2,3]

输出：
2

说明：
只需要两步即可（每一步将一个元素加一或减一）：

[1,2,3]  =>  [2,2,3]  =>  [2,2,2]
```

例2:
```
输入：
[1,2]

输出：
1

说明：
只需要一步即可（每一步将一个元素加一或减一）：

[1,2]  =>  [2,2]
```
 ### 参考代码
 先找到数组的中位值，查找过程基于快速排序的思想，再计算所有的数与中位数之差的和作为结果。
```java
public class Solution {
    public int minMoves2(int[] nums) {

        int median = quickselect(nums, 0, nums.length-1, (nums.length + 1) / 2);
        int minmoves = 0;

        for(int i = 0; i < nums.length; ++ i){
            minmoves += Math.abs( median - nums[i] );
        }
        return minmoves;
    }
    private int quickselect(int[] nums, int start, int end, int size) {
        int mid = (start + end) / 2;
        int pivot = nums[mid];
        int i = start - 1, j = end + 1;
        for (int k = start; k < j; k++) {
            if (nums[k] < pivot) {
                i++;
                swap(nums[i],nums[k]);
            } else if (nums[k] > pivot) {
                j--;
                swap(nums[j],nums[k]);
                k--;
            }
        }
        if (i - start + 1 >= size) {
            return quickselect(nums, start, i, size);
        } else if (j - start >= size) {
            return nums[j-1];
        } else {
            return quickselect(nums, j, end, size - (j - start));
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
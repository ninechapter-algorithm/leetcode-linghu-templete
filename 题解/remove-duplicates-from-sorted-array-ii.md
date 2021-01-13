# 删除排序数组中的重复数字 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-duplicates-from-sorted-array-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个排序数组，删除其中的重复元素，使得每个数字最多出现两次，返回新的数组的长度。
如果一个数字出现超过2次，则这个数字最后保留两个。
 ### 样例说明
 ```
样例 1:
	输入: []
	输出: 0


样例 2:
	输入:  [1,1,1,2,2,3]
	输出: 5
	
	样例解释: 
	长度为 5，  数组为：[1,1,2,2,3]
```
 ### 参考代码
 从重复的第三个开始删除即可
```java
public class Solution {
    /**
     * @param A: a array of integers
     * @return : return an integer
     */
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int index = 0, count = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[index]) {
                if (count < 2) {
                    nums[++index] = nums[i];
                    count ++;
                }
            } else {
                nums[++index] = nums[i];
                count = 1;
            }
        }
        return index + 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 摆动排序
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/wiggle-sort/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个没有排序的数组，请将原数组**就地**重新排列满足如下性质

```
nums[0] <= nums[1] >= nums[2] <= nums[3]....
```

 ### 样例说明
 **样例 1:**

```
输入: [3, 5, 2, 1, 6, 4]
输出: [1, 6, 2, 5, 3, 4]
解释: 这个问题可能有多种答案, [2, 6, 1, 5, 3, 4] 同样可以.
```

**样例 2:**

```
输入: [1, 2, 3, 4]
输出: [1, 4, 2, 3]
```
 ### 参考代码
 从左到右扫一遍，不满足条件的交换就好了。
需要证明的是，当我们 交换了 `nums[i]` 和 `nums[i - 1]` 以后：

```
... nums[i - 2], nums[i], nums[i - 1]
```

nums[i - 2] 不会和 nums[i] 形成逆序（不满足条件的大小关系）

那假如原来是 nums[i - 2] <= nums[i - 1]，那么 nums[i - 1] 和 nums[i] 交换的条件是，nums[i - 1] <= nums[i]。
那我们就推导出此时 nums[i] >= nums[i - 2]，因此交换之后，不会让 nums[i] 和 nums[i - 2] 的大小关系出现变化。

反过来如果 nums[i - 2] >= nums[i - 1] 的情况同理。

---

或者, 老老实实快排(不需要额外空间的 nlogn 的排序算法), 然后从第2个数开始两两交换.
```java
public class Solution {
    /**
     * @param nums a list of integer
     * @return void
     */
    public void wiggleSort(int[] nums) {
        // Write your code here
        for(int i=1; i<nums.length; i++) {
            if((i%2==1 && (nums[i] < nums[i-1]) || 
              (i%2==0) && (nums[i] > nums[i-1]))) {
                swap(nums, i-1, i);
            }
        }
    }
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)
# 寻找旋转排序数组中的最小值 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>假设一个旋转排序的数组其起始位置是未知的（比如<span style="font-weight: 700;"><font color="#e76363">0 1 2 4 5 6 7</font></span>&nbsp;可能变成是<font color="#e76363"><span style="font-weight: 700;">4 5 6 7 0 1 2</span></font>）。</p><p>你需要找到其中最小的元素。</p>
 ### 样例说明
 **样例 1:**
```
输入 :[2,1]
输出 : 1.
```

**样例 2:**
```
输入 :[4,4,5,6,7,0,1,2]
输出: 0.
```
 ### 参考代码
 <p><a href="http://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array-ii/" target="_blank">http://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array-ii/</a><br></p>
```java
// version 1: just for loop is enough
public class Solution {
    public int findMin(int[] num) {
        //  这道题目在面试中不会让写完整的程序
        //  只需要知道最坏情况下 [1,1,1....,1] 里有一个0
        //  这种情况使得时间复杂度必须是 O(n)
        //  因此写一个for循环就好了。
        //  如果你觉得，不是每个情况都是最坏情况，你想用二分法解决不是最坏情况的情况，那你就写一个二分吧。
        //  反正面试考的不是你在这个题上会不会用二分法。这个题的考点是你想不想得到最坏情况。
        int min = num[0];
        for (int i = 1; i < num.length; i++) {
            if (num[i] < min)
                min = num[i];
        }
        return min;
    }
}

// version 2: use *fake* binary-search
public class Solution {
    /**
     * @param num: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == nums[end]) {
                // if mid equals to end, that means it's fine to remove end
                // the smallest element won't be removed
                end--;
            } else if (nums[mid] < nums[end]) {
                end = mid;
                // of course you can merge == & <
            } else {
                start = mid;
                // or start = mid + 1
            }
        }
        
        if (nums[start] <= nums[end]) {
            return nums[start];
        }
        return nums[end];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)